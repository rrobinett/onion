include_directories (${PROJECT_SOURCE_DIR}/src) 

remove_definitions(-DHAVE_PTHREADS)
remove_definitions(-DHAVE_GNUTLS)

add_executable(otemplate otemplate.c parser.c tags.c variables.c list.c functions.c tag_builtins.c load.c
							../../src/onion/log.c ../../src/onion/block.c ../../src/onion/codecs.c ../../src/onion/dict.c ../../src/onion/low.c 
							../common/updateassets.c)

# Template-tag plugins resolve tag_add(), tag_value_arg(), and other
# functions from the otemplate executable when loaded with dlopen().
set_target_properties(otemplate PROPERTIES ENABLE_EXPORTS TRUE)
if(CMAKE_SYSTEM_NAME STREQUAL "Linux")
  target_link_libraries(otemplate PRIVATE dl)
endif()
install(TARGETS otemplate DESTINATION ${CMAKE_INSTALL_BINDIR})

add_subdirectory(templatetags)
# otemplate is not usable for i18n templates until its plugin exists.
add_dependencies(otemplate i18n)
