find_package(opentelemetry-cpp CONFIG REQUIRED)
find_package(gRPC CONFIG REQUIRED)
find_package(Protobuf REQUIRED)
find_package(nlohmann_json REQUIRED)
find_package(CURL REQUIRED)
find_package(absl REQUIRED)

add_executable(
    UrlShortenService
    UrlShortenService.cpp
    ${THRIFT_GEN_CPP_DIR}/UrlShortenService.cpp
    ${THRIFT_GEN_CPP_DIR}/social_network_types.cpp
)

target_include_directories(
    UrlShortenService PRIVATE
    ${LIBMEMCACHED_INCLUDE_DIR}
    ${MONGOC_INCLUDE_DIRS}
    /usr/local/include/jaegertracing
    ${OPENTELEMETRY_CPP_INCLUDE_DIRS}
)

target_link_libraries(
    UrlShortenService
    nlohmann_json::nlohmann_json
    ${MONGOC_LIBRARIES}
    ${LIBMEMCACHED_LIBRARIES}
    ${THRIFT_LIB}
    ${CMAKE_THREAD_LIBS_INIT}
    ${Boost_LIBRARIES}
    Boost::log
    Boost::log_setup
    jaegertracing
    ${OPENTELEMETRY_CPP_LIBRARIES}
)

install(TARGETS UrlShortenService DESTINATION ./)