
# This file was gererated by the build system used internally in the Yandex monorepo.
# Only simple modifications are allowed (adding source-files to targets, adding simple properties
# like target_include_directories). These modifications will be ported to original
# ya.make files by maintainers. Any complex modifications which can't be ported back to the
# original buildsystem will not be accepted.



add_library(private-libs-init INTERFACE)
target_link_libraries(private-libs-init INTERFACE
  contrib-libs-cxxsupp
  yutil
)

add_global_library_for(private-libs-init.global private-libs-init)
target_link_libraries(private-libs-init.global PUBLIC
  contrib-libs-cxxsupp
  yutil
)
target_sources(private-libs-init.global PRIVATE
  ${CMAKE_SOURCE_DIR}/catboost/private/libs/init/init_reg.cpp
)
