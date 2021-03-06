cmake_minimum_required(VERSION 3.14)
project(progetto_prova)

set(CMAKE_CXX_STANDARD 14)

include_directories(.)
set(CMAKE_CXX_FLAGS "--coverage")
set(CMAKE_AUTOMOC ON)
set(CMAKE_AUTOUIC ON)
set(CMAKE_AUTORCC ON)

find_package(Boost CONFIG REQUIRED COMPONENTS regex)
find_package(Boost CONFIG REQUIRED COMPONENTS thread)
find_package(Qt5Core REQUIRED)
find_package(Qt5Gui REQUIRED)
find_package(Qt5Widgets REQUIRED)
find_package(Qt5PrintSupport REQUIRED)
find_package(Qt5Sql REQUIRED)

list(APPEND LIBRARIES
        Qt5::Core
        Qt5::Gui
        Qt5::Widgets
        Qt5::PrintSupport
        Qt5::Sql)
list(REMOVE_DUPLICATES LIBRARIES)
add_executable(progetto_prova main.cpp prova.pro prova.pro.user textedit.cpp Headers/textedit.h
        Headers/stacked.h stacked.cpp Client.cpp Headers/Client.h message.cpp Headers/message.h
        userpage.cpp Headers/userpage.h
        Libs/md5.cpp Libs/md5.h
        Headers/customcursor.h customcursor.cpp
        Headers/Symbol.h Symbol.cpp
        Headers/MessageSymbol.h MessageSymbol.cpp
        project_icons.qrc Style.cpp Headers/Style.h
        myqtextedit.h myqtextedit.cpp)

#target_link_libraries(DBMSProject ${Boost_LIBRARIES})  # that didn't work

target_link_libraries(progetto_prova ${LIBRARIES})
target_link_libraries(progetto_prova Boost::thread)
target_link_libraries(progetto_prova Boost::regex)
if(MSVC OR MINGW)
    target_link_libraries(progetto_prova ws2_32 mswsock)
endif()
