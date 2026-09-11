cmake_minimum_required(VERSION 3.22.1)

project(ColorLabeledRegions)

find_package(
  ITK
  REQUIRED
  COMPONENTS
    ITKImageIO
    ITKCommon
    ITKImageFusion
    ITKLabelMap
)
itk_generate_factory_registration()

add_executable(${PROJECT_NAME} Code.cxx)
target_link_libraries(
  ${PROJECT_NAME}
  PRIVATE
    ${ITK_INTERFACE_LIBRARIES}
    ITK::ITKImageIO
)

install(
  TARGETS
    ${PROJECT_NAME}
  DESTINATION bin/ITKSphinxExamples/Filtering/ImageFusion
  COMPONENT Runtime
)

install(
  FILES
    Code.cxx
    CMakeLists.txt
  DESTINATION
    share/ITKSphinxExamples/Code/Filtering/ImageFusion/ColorLabeledRegions/
  COMPONENT Code
)

enable_testing()
add_test(
  NAME ColorLabeledRegionsTest
  COMMAND
    ${CMAKE_RUNTIME_OUTPUT_DIRECTORY}/${PROJECT_NAME}
)
