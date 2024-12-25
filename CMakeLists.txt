cmake_minimum_required(VERSION 3.30)
project(AudioPortLibsnd LANGUAGES CXX C)
set(CMAKE_CXX_STANDARD 20)
set(CMAKE_RUNTIME_OUTPUT_DIRECTORY ${CMAKE_BINARY_DIR}/bin)

# Fetch PortAudio
include(FetchContent)
FetchContent_Declare(
    portaudio
    GIT_REPOSITORY https://github.com/PortAudio/portaudio.git
    GIT_TAG v19.7.0
    GIT_SHALLOW ON
)
FetchContent_MakeAvailable(portaudio)

# Fetch Libsndfile
include(FetchContent)
FetchContent_Declare(
    libsndfile
    GIT_REPOSITORY https://github.com/libsndfile/libsndfile
    GIT_TAG 1.2.2
    GIT_SHALLOW ON
)
FetchContent_MakeAvailable(libsndfile)

# Fetch wxWidgets
include(FetchContent)
FetchContent_Declare(
    wxWidgets
    GIT_REPOSITORY https://github.com/wxWidgets/wxWidgets
    GIT_TAG v3.2.6
    GIT_SHALLOW ON
)
FetchContent_MakeAvailable(wxWidgets)

# Add the main executable
add_executable(main Project/main.cpp)

# Set subsystem to Windows for GUI applications
if(WIN32)
    set_target_properties(main PROPERTIES WIN32_EXECUTABLE ON)
endif()

# Link libraries
target_link_libraries(main PRIVATE portaudio sndfile wx::net wx::core wx::base)
