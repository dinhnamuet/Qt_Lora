cmake_minimum_required(VERSION 3.16)

project(application VERSION 0.1 LANGUAGES CXX)

set(CMAKE_CXX_STANDARD_REQUIRED ON)

find_package(Qt6 6.4 REQUIRED COMPONENTS Quick)
find_package(Qt6 REQUIRED COMPONENTS Charts)
qt_standard_project_setup()

set(app_icon_resource_windows "${CMAKE_CURRENT_SOURCE_DIR}/Image_Folder/uet_logo.rc")

qt_add_executable(appapplication
    main.cpp
    ${app_icon_resource_windows}
)

qt_add_qml_module(appapplication
    URI application
    VERSION 1.0
    QML_FILES Main.qml
RESOURCES Image_Folder/a.jpg Image_Folder/connect.png Image_Folder/drawer.png Image_Folder/images.jpeg Image_Folder/images.png Image_Folder/Lora.png Image_Folder/operation.png Image_Folder/uet_logo.ico Image_Folder/uet_logo.png Image_Folder/uet_logo.rc
QML_FILES Qml_Folder/Drawer_Custom.qml Qml_Folder/Header_GUI.qml Qml_Folder/Node_GUI.qml Qml_Folder/Socket_GUI.qml
SOURCES backend.h backend.cpp
)

# Qt for iOS sets MACOSX_BUNDLE_GUI_IDENTIFIER automatically since Qt 6.1.
# If you are developing for iOS or macOS you should consider setting an
# explicit, fixed bundle identifier manually though.
set_target_properties(appapplication PROPERTIES
#    MACOSX_BUNDLE_GUI_IDENTIFIER com.example.appapplication
    MACOSX_BUNDLE_BUNDLE_VERSION ${PROJECT_VERSION}
    MACOSX_BUNDLE_SHORT_VERSION_STRING ${PROJECT_VERSION_MAJOR}.${PROJECT_VERSION_MINOR}
    MACOSX_BUNDLE TRUE
    WIN32_EXECUTABLE TRUE
)

target_link_libraries(appapplication
    PRIVATE Qt6::Quick
    PRIVATE Qt6::Charts
)

include(GNUInstallDirs)
install(TARGETS appapplication
    BUNDLE DESTINATION .
    LIBRARY DESTINATION ${CMAKE_INSTALL_LIBDIR}
    RUNTIME DESTINATION ${CMAKE_INSTALL_BINDIR}
)
