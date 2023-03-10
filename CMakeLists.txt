cmake_minimum_required(VERSION 3.0.0)
project(execs VERSION 0.1.0)

set(CMAKE_CXX_STANDARD 17)
set(CMAKE_CXX_EXTENSIONS off)
set(CMAKE_CXX_STANDARD_REQUIRED on)

include(CTest)
enable_testing()

find_package(GDAL CONFIG REQUIRED)
find_package(spdlog CONFIG REQUIRED)

set(CPACK_PROJECT_NAME ${PROJECT_NAME})
set(CPACK_PROJECT_VERSION ${PROJECT_VERSION})
include(CPack)

# 空值转换为指定数值
add_executable(_nan_TransTo nan_transto.cpp template_nan_convert_to.h)
target_link_libraries(_nan_TransTo PRIVATE GDAL::GDAL)
target_link_libraries(_nan_TransTo PRIVATE spdlog::spdlog spdlog::spdlog_header_only)

# setNoDataValue 去黑边
add_executable(_set_NoData_Value set_nodata_value.cpp)
target_link_libraries(_set_NoData_Value PRIVATE GDAL::GDAL)
target_link_libraries(_set_NoData_Value PRIVATE spdlog::spdlog spdlog::spdlog_header_only)

# float格式（不止）的二进制影像转换为tif并输出
add_executable(_binary_to_tif binary_img_to_tif.cpp template_binary_img_io.h)
target_link_libraries(_binary_to_tif PRIVATE GDAL::GDAL)
target_link_libraries(_binary_to_tif PRIVATE spdlog::spdlog spdlog::spdlog_header_only)

# tif转换为二进制格式
add_executable(_tif_to_binary tif_to_binary.cpp template_binary_img_io.h)
target_link_libraries(_tif_to_binary PRIVATE GDAL::GDAL)
target_link_libraries(_tif_to_binary PRIVATE spdlog::spdlog spdlog::spdlog_header_only)

# 统计影像信息
add_executable(_statistics statistics.cpp)
target_link_libraries(_statistics PRIVATE GDAL::GDAL)
target_link_libraries(_statistics PRIVATE spdlog::spdlog spdlog::spdlog_header_only)

#百分比拉伸
add_executable(_histogram_stretch histogram_stretch.cpp template_stretch.h)
target_link_libraries(_histogram_stretch PRIVATE GDAL::GDAL)
target_link_libraries(_histogram_stretch PRIVATE spdlog::spdlog spdlog::spdlog_header_only)
