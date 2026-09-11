cmake_minimum_required(VERSION 3.22.1)

project(StatisticalPropertiesOfRegions)

find_package(
  ITK
  REQUIRED
  COMPONENTS
    ITKImageIO
    ITKCommon
    ITKImageStatistics
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
  DESTINATION bin/ITKSphinxExamples/Filtering/ImageStatistics
  COMPONENT Runtime
)

install(
  FILES
    Code.cxx
    CMakeLists.txt
  DESTINATION
    share/ITKSphinxExamples/Code/Filtering/ImageStatistics/StatisticalPropertiesOfRegions/
  COMPONENT Code
)

enable_testing()
add_test(
  NAME StatisticalPropertiesOfRegionsTest
  COMMAND
    ${CMAKE_RUNTIME_OUTPUT_DIRECTORY}/${PROJECT_NAME}
)
