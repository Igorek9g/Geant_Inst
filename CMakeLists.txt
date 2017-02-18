cmake_minimum_required(VERSION 3.6)
project(geant4first)

set(CMAKE_CXX_STANDARD 11)
set(CMAKE_PREFIX_PATH /home/idalov/geant4/geant4_10_03-install)

option(WITH_GEANT4_UIVITS "Build with Geant4 UI and Vis drivers" ON)

if(WITH_GEANT4_UIVIS)
    find_package(Geant4 REQUIRED ui_all vis_all)
else()
    find_package(Geant4 REQUIRED)
endif()

include(${Geant4_USE_FILE})

include_directories(${PROJECT_SOURCE_DIR}/include)

file(GLOB sources ${PROJECT_SOURCE_DIR}/src/*.cpp)
file(GLOB headers ${PROJECT_SOURCE_DIR}/include/*.h)

add_executable(geant4first main.cpp ${sources} ${headers})

target_link_libraries(geant4first ${Geant4_LIBRARIES})

install(TARGETS geant4first DESTINATION bin)