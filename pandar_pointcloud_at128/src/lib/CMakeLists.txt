add_library(pandar_rawdata_at128 rawdata.cc calibration.cc)
add_dependencies(pandar_rawdata_at128 ${${PROJECT_NAME}_EXPORTED_TARGETS})
target_link_libraries(pandar_rawdata_at128 
                      ${catkin_LIBRARIES}
                      ${YAML_CPP_LIBRARIES})
install(TARGETS pandar_rawdata_at128
        RUNTIME DESTINATION ${CATKIN_PACKAGE_BIN_DESTINATION}
        ARCHIVE DESTINATION ${CATKIN_PACKAGE_LIB_DESTINATION}
        LIBRARY DESTINATION ${CATKIN_PACKAGE_LIB_DESTINATION})
set_property(TARGET pandar_rawdata_at128 PROPERTY CXX_STANDARD 14)

add_library(pandar_input_at128 input.cc platUtil.cc fault_message.cc)
target_link_libraries(pandar_input_at128
  ${catkin_LIBRARIES}
  ${libpcap_LIBRARIES}
)
if(catkin_EXPORTED_TARGETS)
  add_dependencies(pandar_input_at128 ${catkin_EXPORTED_TARGETS})
endif()

install(TARGETS pandar_input_at128
        LIBRARY DESTINATION ${CATKIN_PACKAGE_LIB_DESTINATION}
)
