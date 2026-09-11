cmake_minimum_required(VERSION 3.22.1)

project(LabelConnectComponentsInBinaryImage)

find_package(
  ITK
  REQUIRED
  COMPONENTS
    ITKImageIO
    ITKConnectedComponents
    ITKImageFusion
    ITKThresholding
)
itk_generate_factory_registration()

add_executable(${PROJECT_NAME} Code.cxx)
target_link_libraries(
  ${PROJECT_NAME}
  PRIVATE
    ${ITK_INTERFACE_LIBRARIES}
    ITK::ITKImageIO
    ITK::ITKVtkGlueModule
)

install(
  TARGETS
    ${PROJECT_NAME}
  DESTINATION bin/ITKSphinxExamples/Segmentation/ConnectedComponents
  COMPONENT Runtime
)

install(
  FILES
    Code.cxx
    CMakeLists.txt
  DESTINATION
    share/ITKSphinxExamples/Code/Segmentation/ConnectedComponents/LabelConnectComponentsInBinaryImage/
  COMPONENT Code
)

enable_testing()
add_test(
  NAME LabelConnectComponentsInBinaryImageTest
  COMMAND
    ${CMAKE_RUNTIME_OUTPUT_DIRECTORY}/${PROJECT_NAME}
)
