cmake_minimum_required(VERSION 3.11)

project(bookypedia CXX)
set(CMAKE_CXX_STANDARD 20)

include(${CMAKE_BINARY_DIR}/conanbuildinfo_multi.cmake)
conan_basic_setup(TARGETS)

set(THREADS_PREFER_PTHREAD_FLAG ON)
find_package(Threads REQUIRED)

add_library(libbookypedia STATIC
	src/menu/menu.cpp
	src/menu/menu.h
	src/ui/view.cpp
	src/ui/view.h
	src/app/use_cases.h
	src/app/use_cases_impl.cpp
	src/app/use_cases_impl.h
	src/app/unit_of_work.h
	src/domain/author.cpp
	src/domain/author.h
	src/domain/author_fwd.h
	src/domain/book.cpp
	src/domain/book.h
	src/domain/book_fwd.h
	src/domain/book_tag.cpp
	src/domain/book_tag.h
	src/domain/book_tag_fwd.h
	src/util/tagged.h
	src/util/tagged_uuid.cpp
	src/util/tagged_uuid.h
	src/util/overload_pattern.h
	src/postgres/postgres.cpp
	src/postgres/postgres.h
)
target_link_libraries(libbookypedia PUBLIC CONAN_PKG::boost Threads::Threads CONAN_PKG::libpq CONAN_PKG::libpqxx)

add_executable(bookypedia
	src/bookypedia.cpp
	src/bookypedia.h
	src/main.cpp
)
target_link_libraries(bookypedia PRIVATE CONAN_PKG::boost libbookypedia)