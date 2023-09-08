include_directories(../taskflow)

find_package(PCL REQUIRED COMPONENTS common)
find_package(OpenSSL REQUIRED)

message("OpenSSL include dir: ${OPENSSL_INCLUDE_DIR}")

include_directories(
	${OPENSSL_INCLUDE_DIR}
)

add_executable(pandar_cloud_node_at128 cloud_node.cc convert.cc driver.cc laser_ts.cpp tcp_command_client.c util.c)
add_dependencies(pandar_cloud_node_at128 ${${PROJECT_NAME}_EXPORTED_TARGETS})
target_link_libraries(pandar_cloud_node_at128 pandar_rawdata_at128
					  pandar_input_at128
					  pcap
					  ${OPENSSL_LIBRARIES}
					  ${PCL_INCLUDE_DIRS}
                      ${catkin_LIBRARIES} ${YAML_CPP_LIBRARIES})
					  

add_library(pandar_cloud_nodelet_at128 cloud_nodelet.cc convert.cc driver.cc laser_ts.cpp tcp_command_client.c util.c)
add_dependencies(pandar_cloud_nodelet_at128 ${${PROJECT_NAME}_EXPORTED_TARGETS})
target_link_libraries(pandar_cloud_nodelet_at128 
					  pandar_rawdata_at128 
					  pandar_input_at128
					  pcap
					  ${OPENSSL_LIBRARIES}
					  ${PCL_INCLUDE_DIRS}
                      ${catkin_LIBRARIES} ${YAML_CPP_LIBRARIES})

add_executable(pandar_transform_node_at128 transform_node.cc transform.cc convert.cc driver.cc laser_ts.cpp tcp_command_client.c util.c)
add_dependencies(pandar_transform_node_at128 ${${PROJECT_NAME}_EXPORTED_TARGETS})
target_link_libraries(pandar_transform_node_at128 pandar_rawdata_at128
						pandar_input_at128
						pcap
						${OPENSSL_LIBRARIES}
						${PCL_INCLUDE_DIRS}
					  	${catkin_LIBRARIES} ${YAML_CPP_LIBRARIES})

add_library(pandar_transform_nodelet_at128 transform_nodelet.cc transform.cc convert.cc driver.cc laser_ts.cpp tcp_command_client.c util.c)
add_dependencies(pandar_transform_nodelet_at128 ${${PROJECT_NAME}_EXPORTED_TARGETS})
target_link_libraries(pandar_transform_nodelet_at128 pandar_rawdata_at128
						pandar_input_at128
						pcap
						${OPENSSL_LIBRARIES}
						${PCL_INCLUDE_DIRS}
					  ${catkin_LIBRARIES} ${YAML_CPP_LIBRARIES})
install(TARGETS 
            pandar_cloud_node_at128
            pandar_cloud_nodelet_at128
            pandar_transform_node_at128
            pandar_transform_nodelet_at128
		RUNTIME DESTINATION ${CATKIN_PACKAGE_BIN_DESTINATION}
		ARCHIVE DESTINATION ${CATKIN_PACKAGE_LIB_DESTINATION}
		LIBRARY DESTINATION ${CATKIN_PACKAGE_LIB_DESTINATION})