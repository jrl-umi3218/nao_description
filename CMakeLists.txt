cmake_minimum_required(VERSION 2.8.3)
project(nao_description)

find_package(catkin REQUIRED COMPONENTS xacro)

# Configure the develspace pkg-config file
set(DATADIR "${PROJECT_SOURCE_DIR}")
configure_file(
  "${PROJECT_SOURCE_DIR}/${PROJECT_NAME}.pc.cmake"
  "${CATKIN_DEVEL_PREFIX}/lib/pkgconfig/${PROJECT_NAME}.pc")

# Configure the installspace pkg-config file
set(DATADIR "${CMAKE_INSTALL_PREFIX}/${CATKIN_PACKAGE_SHARE_DESTINATION}")
file(MAKE_DIRECTORY ${CMAKE_CURRENT_BINARY_DIR}/catkin_generated/installspace)
configure_file(
  "${PROJECT_SOURCE_DIR}/${PROJECT_NAME}.pc.cmake"
  "${CMAKE_CURRENT_BINARY_DIR}/catkin_generated/installspace/${PROJECT_NAME}.pc")
install(
  FILES ${CMAKE_CURRENT_BINARY_DIR}/catkin_generated/installspace/${PROJECT_NAME}.pc
  DESTINATION lib/pkgconfig)

catkin_python_setup()

install(DIRECTORY urdf/
	DESTINATION ${CATKIN_PACKAGE_SHARE_DESTINATION}/urdf
	PATTERN "*.xacro" EXCLUDE)

install(DIRECTORY convex/
	DESTINATION ${CATKIN_PACKAGE_SHARE_DESTINATION}/convex)

install(DIRECTORY stpbv/
	DESTINATION ${CATKIN_PACKAGE_SHARE_DESTINATION}/stpbv)

install(DIRECTORY meshes/
	DESTINATION ${CATKIN_PACKAGE_SHARE_DESTINATION}/meshes)

install(DIRECTORY rsdf/
	DESTINATION ${CATKIN_PACKAGE_SHARE_DESTINATION}/rsdf)

install(DIRECTORY surfaces/
	DESTINATION ${CATKIN_PACKAGE_SHARE_DESTINATION}/surfaces)
