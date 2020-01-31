add_library(tbsgNetLib STATIC)
target_sources_local(
    tbsgNetLib
    PRIVATE
    Crypto/NetRSA.cpp
    Crypto/NetAES.cpp
    Net/win/WINPacket.cpp
    Net/Client.cpp
    Net/Connection.cpp
    Net/Server.cpp
    Utility/Utils.cpp
    )
target_include_directories(tbsgNetLib
    PRIVATE ${CMAKE_CURRENT_SOURCE_DIR}
    PRIVATE ${PROJECT_SOURCE_DIR}/third_party/mariadb/include/mysql
    PUBLIC ${PROJECT_SOURCE_DIR}/include
    PUBLIC $<BUILD_INTERFACE:${PROJECT_SOURCE_DIR}/third_party/enet/include>
    )

target_link_libraries(tbsgNetLib 
    PUBLIC
    openssl
    enet
    ptl
    ws2_32.lib
    winmm.lib
        ${PROJECT_SOURCE_DIR}/third_party/openssl/lib/libcrypto.lib
        ${PROJECT_SOURCE_DIR}/third_party/openssl/lib/libssl.lib
    ${PROJECT_SOURCE_DIR}/third_party/mariadb/lib/libmariadb.lib
    ${PROJECT_SOURCE_DIR}/third_party/mariadb/lib/mariadbclient.lib
    FlatValueMap
    BasicLogger
)

    add_library(databaseAPI STATIC)
    target_sources_local(
        databaseAPI
        PRIVATE
        databaseAPI/DatabaseAPI.cpp
        databaseAPI/GameDataDatabase.cpp
        databaseAPI/ProfileDatabase.cpp
        )
    target_include_directories(databaseAPI
        PRIVATE ${CMAKE_CURRENT_SOURCE_DIR}
        PUBLIC ${PROJECT_SOURCE_DIR}/include/
        PUBLIC ${PROJECT_SOURCE_DIR}/include/databaseAPI
        PUBLIC ${PROJECT_SOURCE_DIR}/third_party/mariadb/include/mysql
        PUBLIC ${PROJECT_SOURCE_DIR}/third_party/mariadb/include
        PUBLIC $<BUILD_INTERFACE:${PROJECT_SOURCE_DIR}/third_party/enet/include>
        )
        target_link_libraries(databaseAPI 
        PUBLIC
        ptl
        openssl
        ${PROJECT_SOURCE_DIR}/third_party/openssl/lib/libcrypto.lib
        ${PROJECT_SOURCE_DIR}/third_party/openssl/lib/libssl.lib
        ${PROJECT_SOURCE_DIR}/third_party/mariadb/lib/libmariadb.lib
        ${PROJECT_SOURCE_DIR}/third_party/mariadb/lib/mariadbclient.lib
        FlatValueMap
        BasicLogger
    )
