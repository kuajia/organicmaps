project(pygen)

set(
  SRC
  pygen.cpp
)

include_directories(${CMAKE_BINARY_DIR})

omim_add_library(${PROJECT_NAME} MODULE ${SRC})

find_package(EXPAT REQUIRED)
omim_link_libraries(
  ${PROJECT_NAME}
  generator
  routing
  traffic
  routing_common
  descriptions
  transit
  search
  storage
  editor
  indexer
  mwm_diff
  platform
  geometry
  coding
  base
  opening_hours
  freetype
  ${EXPAT_LIBRARIES}
  ICU::i18n
  cppjansson
  protobuf
  bsdiff
  minizip
  succinct
  pugixml
  tess2
  sqlite3
  ${CMAKE_DL_LIBS}
  ZLIB::ZLIB
  ${Boost_LIBRARIES}
)

link_qt5_core(${PROJECT_NAME})
link_qt5_network(${PROJECT_NAME})

if (PLATFORM_MAC)
  omim_link_libraries(${PROJECT_NAME} "-Wl,-undefined,dynamic_lookup")
endif()

set_target_properties(${PROJECT_NAME} PROPERTIES PREFIX "")
