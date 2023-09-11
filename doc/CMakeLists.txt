find_package ( Doxygen REQUIRED )

# Copy doxy.config.in
configure_file(
  ${PROJECT_SOURCE_DIR}/doc/Doxyfile.in
  ${CMAKE_CURRENT_BINARY_DIR}/Doxyfile
)

configure_file(
  ${PROJECT_SOURCE_DIR}/doc/Doxyfile.xml.in
  ${CMAKE_CURRENT_BINARY_DIR}/Doxyfile.xml
)

# Run doxygen
add_custom_command(
  OUTPUT ${CMAKE_CURRENT_BINARY_DIR}/html/index.html
  COMMAND ${DOXYGEN_EXECUTABLE} ${CMAKE_CURRENT_BINARY_DIR}/Doxyfile
  COMMENT "Generating API documentation"
  DEPENDS ${c_headers};${c_sources};${cpp_sources};${cpp_headers}
)

add_custom_target(
  docs ALL
  COMMENT "Documentation target docs"
  DEPENDS ${CMAKE_CURRENT_BINARY_DIR}/html/index.html
)
