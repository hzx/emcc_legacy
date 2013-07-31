cmake_minimum_required(VERSION 2.8.7)
project(emcc_exp)

include_directories(${PROJECT_SOURCE_DIR})

set(APP_NAME
  app
  )

set(APP_OUT
  ${PROJECT_BINARY_DIR}/${APP_NAME}.js
  )

set(APP_SRC
  main.cpp
  )

set(APP_DEPENDS
  ${APP_SRC}
  )

add_custom_command(
  OUTPUT ${APP_OUT}
  COMMAND emcc
    #-std=c++11
    -o ${APP_OUT}
    --bind
    --typed-arrays 0
    ${APP_SRC}
  WORKING_DIRECTORY ${PROJECT_SOURCE_DIR}
  DEPENDS ${APP_DEPENDS}
  )
add_custom_target(${APP_NAME} ALL DEPENDS ${APP_DEPENDS} ${APP_OUT})

configure_file(
  ${PROJECT_SOURCE_DIR}/app.html
  ${PROJECT_BINARY_DIR}/app.html
  COPYONLY
  )
