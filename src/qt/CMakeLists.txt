CMAKE_MINIMUM_REQUIRED(VERSION 3.14)

set(QT_MINIMUM_VERSION 5.5.1)
set(CMAKE_INCLUDE_CURRENT_DIR ON)
set(CMAKE_AUTOUIC_SEARCH_PATHS ${CMAKE_CURRENT_SOURCE_DIR}/forms ${CMAKE_CURRENT_SOURCE_DIR}/lats/forms ${CMAKE_CURRENT_SOURCE_DIR}/lats/settings/forms)
set(CMAKE_AUTOMOC ON)
set(CMAKE_AUTORCC ON)
set(CMAKE_AUTOUIC ON)

if (${CMAKE_SYSTEM_NAME} MATCHES "Linux")
    set(CMAKE_POSITION_INDEPENDENT_CODE ON)
endif ()

unset(Qt5Enables)
foreach(comp Widgets Core Gui Network LinguistTools DBus Svg Charts)
    find_package(Qt5${comp})
    set(Qt5Enables "${Qt5Enables};Qt5${comp}_FOUND")
    if(Qt5${comp}_FOUND)
        MESSAGE(STATUS "FOUND Qt5${comp}")
        include_directories(${include_directories} ${Qt5${comp}_INCLUDE_DIRS} ${QT_USE_FILE})
        add_definitions(${Qt5${comp}_DEFINITIONS})
        list(APPEND Qt5_LIBRARIES ${Qt5${comp}_LIBRARIES})
    else()
        MESSAGE(WARNING "Cant find Qt5${comp}")
    endif()
endforeach(comp)

if (Qt5Core_FOUND)
    if (Qt5Core_VERSION VERSION_LESS QT_MINIMUM_VERSION)
        MESSAGE(FATAL_ERROR "Minimum supported Qt5 version is ${QT_MINIMUM_VERSION}")
    else()
        MESSAGE(STATUS "Found Qt5 version: ${Qt5Core_VERSION}")
    endif()
else()
    MESSAGE(FATAL_ERROR "Could not find any Qt5 installation")
endif()

if (Qt5DBus_FOUND)
    add_compile_options("-DUSE_DBUS")
endif()

if (Qt5Charts_FOUND)
    add_compile_options("-DUSE_QTCHARTS")
endif()

find_package(Qrcode)
if (QRCODE_FOUND)
    include_directories ( ${QRCODE_INCLUDE_DIR} )
    link_directories ( ${QRCODE_LIBRARY_DIRS} )
endif()

add_compile_options("-DQT_NO_KEYWORDS")

# Why isn't this done automatically??
if (${CMAKE_SYSTEM_NAME} MATCHES "Darwin")
    set(CMAKE_AUTOMOC_MOC_OPTIONS "-DQ_OS_MAC")
endif()

file(GLOB LOCAL_QT_HEADERS ${CMAKE_CURRENT_SOURCE_DIR}/*.h)
source_group("QtHeaders" FILES ${LOCAL_QT_HEADERS})

SET(QT_SOURCES
        ${CMAKE_CURRENT_SOURCE_DIR}/bantablemodel.cpp
        ${CMAKE_CURRENT_SOURCE_DIR}/bitcoinaddressvalidator.cpp
        ${CMAKE_CURRENT_SOURCE_DIR}/bitcoinunits.cpp
        ${CMAKE_CURRENT_SOURCE_DIR}/clientmodel.cpp
        ${CMAKE_CURRENT_SOURCE_DIR}/csvmodelwriter.cpp
        ${CMAKE_CURRENT_SOURCE_DIR}/guiutil.cpp
        ${CMAKE_CURRENT_SOURCE_DIR}/intro.cpp
        ${CMAKE_CURRENT_SOURCE_DIR}/networkstyle.cpp
        ${CMAKE_CURRENT_SOURCE_DIR}/notificator.cpp
        ${CMAKE_CURRENT_SOURCE_DIR}/optionsmodel.cpp
        ${CMAKE_CURRENT_SOURCE_DIR}/peertablemodel.cpp
        ${CMAKE_CURRENT_SOURCE_DIR}/qvalidatedlineedit.cpp
        ${CMAKE_CURRENT_SOURCE_DIR}/qvaluecombobox.cpp
        ${CMAKE_CURRENT_SOURCE_DIR}/rpcconsole.cpp
        ${CMAKE_CURRENT_SOURCE_DIR}/rpcexecutor.cpp
        ${CMAKE_CURRENT_SOURCE_DIR}/trafficgraphwidget.cpp
        ${CMAKE_CURRENT_SOURCE_DIR}/utilitydialog.cpp
        ${CMAKE_CURRENT_SOURCE_DIR}/addressbookpage.cpp
        ${CMAKE_CURRENT_SOURCE_DIR}/addresstablemodel.cpp
        ${CMAKE_CURRENT_SOURCE_DIR}/askpassphrasedialog.cpp
        ${CMAKE_CURRENT_SOURCE_DIR}/coincontroldialog.cpp
        ${CMAKE_CURRENT_SOURCE_DIR}/coincontroltreewidget.cpp
        ${CMAKE_CURRENT_SOURCE_DIR}/editaddressdialog.cpp
        ${CMAKE_CURRENT_SOURCE_DIR}/openuridialog.cpp
        ${CMAKE_CURRENT_SOURCE_DIR}/paymentserver.cpp
        ${CMAKE_CURRENT_SOURCE_DIR}/transactionfilterproxy.cpp
        ${CMAKE_CURRENT_SOURCE_DIR}/transactionrecord.cpp
        ${CMAKE_CURRENT_SOURCE_DIR}/transactiontablemodel.cpp
        ${CMAKE_CURRENT_SOURCE_DIR}/walletmodel.cpp
        ${CMAKE_CURRENT_SOURCE_DIR}/walletmodeltransaction.cpp
        ${CMAKE_CURRENT_SOURCE_DIR}/lats/latsgui.cpp
        ${CMAKE_CURRENT_SOURCE_DIR}/lats/loadingdialog.cpp
        ${CMAKE_CURRENT_SOURCE_DIR}/lats/pwidget.cpp
        ${CMAKE_CURRENT_SOURCE_DIR}/lats/focuseddialog.cpp
        ${CMAKE_CURRENT_SOURCE_DIR}/lats/guitransactionsutils.cpp
        ${CMAKE_CURRENT_SOURCE_DIR}/lats/snackbar.cpp
        ${CMAKE_CURRENT_SOURCE_DIR}/lats/navmenuwidget.cpp
        ${CMAKE_CURRENT_SOURCE_DIR}/lats/lockunlock.cpp
        ${CMAKE_CURRENT_SOURCE_DIR}/lats/receivedialog.cpp
        ${CMAKE_CURRENT_SOURCE_DIR}/lats/furabstractlistitemdelegate.cpp
        ${CMAKE_CURRENT_SOURCE_DIR}/lats/txviewholder.cpp
        ${CMAKE_CURRENT_SOURCE_DIR}/lats/qtutils.cpp
        ${CMAKE_CURRENT_SOURCE_DIR}/lats/balancebubble.cpp
        ${CMAKE_CURRENT_SOURCE_DIR}/lats/expandablebutton.cpp
        ${CMAKE_CURRENT_SOURCE_DIR}/lats/topbar.cpp
        ${CMAKE_CURRENT_SOURCE_DIR}/lats/txrow.cpp
        ${CMAKE_CURRENT_SOURCE_DIR}/lats/addressfilterproxymodel.cpp
        ${CMAKE_CURRENT_SOURCE_DIR}/lats/dashboardwidget.cpp
        ${CMAKE_CURRENT_SOURCE_DIR}/lats/addresslabelrow.cpp
        ${CMAKE_CURRENT_SOURCE_DIR}/lats/contactdropdownrow.cpp
        ${CMAKE_CURRENT_SOURCE_DIR}/lats/contactsdropdown.cpp
        ${CMAKE_CURRENT_SOURCE_DIR}/lats/optionbutton.cpp
        ${CMAKE_CURRENT_SOURCE_DIR}/lats/mninfodialog.cpp
        ${CMAKE_CURRENT_SOURCE_DIR}/lats/coldstakingmodel.cpp
        ${CMAKE_CURRENT_SOURCE_DIR}/lats/mnmodel.cpp
        ${CMAKE_CURRENT_SOURCE_DIR}/lats/masternodewizarddialog.cpp
        ${CMAKE_CURRENT_SOURCE_DIR}/lats/mnrow.cpp
        ${CMAKE_CURRENT_SOURCE_DIR}/lats/masternodeswidget.cpp
        ${CMAKE_CURRENT_SOURCE_DIR}/lats/sendchangeaddressdialog.cpp
        ${CMAKE_CURRENT_SOURCE_DIR}/lats/sendconfirmdialog.cpp
        ${CMAKE_CURRENT_SOURCE_DIR}/lats/sendcustomfeedialog.cpp
        ${CMAKE_CURRENT_SOURCE_DIR}/lats/sendmemodialog.cpp
        ${CMAKE_CURRENT_SOURCE_DIR}/lats/sendmultirow.cpp
        ${CMAKE_CURRENT_SOURCE_DIR}/lats/send.cpp
        ${CMAKE_CURRENT_SOURCE_DIR}/lats/addnewcontactdialog.cpp
        ${CMAKE_CURRENT_SOURCE_DIR}/lats/requestdialog.cpp
        ${CMAKE_CURRENT_SOURCE_DIR}/lats/receivewidget.cpp
        ${CMAKE_CURRENT_SOURCE_DIR}/lats/myaddressrow.cpp
        ${CMAKE_CURRENT_SOURCE_DIR}/lats/csrow.cpp
        ${CMAKE_CURRENT_SOURCE_DIR}/lats/addressholder.cpp
        ${CMAKE_CURRENT_SOURCE_DIR}/lats/tooltipmenu.cpp
        ${CMAKE_CURRENT_SOURCE_DIR}/lats/addresseswidget.cpp
        ${CMAKE_CURRENT_SOURCE_DIR}/lats/defaultdialog.cpp
        ${CMAKE_CURRENT_SOURCE_DIR}/lats/coldstakingwidget.cpp
        ${CMAKE_CURRENT_SOURCE_DIR}/lats/mnselectiondialog.cpp
        ${CMAKE_CURRENT_SOURCE_DIR}/lats/proposalcard.cpp
        ${CMAKE_CURRENT_SOURCE_DIR}/lats/votedialog.cpp
        ${CMAKE_CURRENT_SOURCE_DIR}/lats/createproposaldialog.cpp
        ${CMAKE_CURRENT_SOURCE_DIR}/lats/proposalinfodialog.cpp
        ${CMAKE_CURRENT_SOURCE_DIR}/lats/governancewidget.cpp
        ${CMAKE_CURRENT_SOURCE_DIR}/lats/settings/settingsbackupwallet.cpp
        ${CMAKE_CURRENT_SOURCE_DIR}/lats/settings/settingsbittoolwidget.cpp
        ${CMAKE_CURRENT_SOURCE_DIR}/lats/settings/settingsconsolewidget.cpp
        ${CMAKE_CURRENT_SOURCE_DIR}/lats/settings/settingsdisplayoptionswidget.cpp
        ${CMAKE_CURRENT_SOURCE_DIR}/lats/settings/settingsfaqwidget.cpp
        ${CMAKE_CURRENT_SOURCE_DIR}/lats/settings/settingsinformationwidget.cpp
        ${CMAKE_CURRENT_SOURCE_DIR}/lats/settings/settingsmainoptionswidget.cpp
        ${CMAKE_CURRENT_SOURCE_DIR}/lats/settings/settingssignmessagewidgets.cpp
        ${CMAKE_CURRENT_SOURCE_DIR}/lats/settings/settingswalletoptionswidget.cpp
        ${CMAKE_CURRENT_SOURCE_DIR}/lats/settings/settingswalletrepairwidget.cpp
        ${CMAKE_CURRENT_SOURCE_DIR}/lats/settings/settingsexportcsv.cpp
        ${CMAKE_CURRENT_SOURCE_DIR}/lats/settings/settingswidget.cpp
        ${CMAKE_CURRENT_SOURCE_DIR}/lats/welcomecontentwidget.cpp
        ${CMAKE_CURRENT_SOURCE_DIR}/lats/splash.cpp
        ${CMAKE_CURRENT_SOURCE_DIR}/lats/governancemodel.cpp
        )

qt5_generate_moc(lats/pfborderimage.h ${CMAKE_CURRENT_SOURCE_DIR}/lats/moc_pfborderimage.cpp)
list(APPEND QT_SOURCES ${CMAKE_CURRENT_SOURCE_DIR}/lats/moc_pfborderimage.cpp)

if (${CMAKE_SYSTEM_NAME} MATCHES "Darwin")
    list(APPEND QT_SOURCES ${CMAKE_CURRENT_SOURCE_DIR}/macdockiconhandler.mm)
    list(APPEND QT_SOURCES ${CMAKE_CURRENT_SOURCE_DIR}/macnotificationhandler.mm)
endif()

add_library(qt_stuff STATIC ${BitcoinHeaders} ${QtHeaders} ${QT_SOURCES} ${PROTO_SRCS} ${PROTO_HDRS})
target_include_directories(qt_stuff PUBLIC ${CMAKE_SOURCE_DIR}/src
        ${CMAKE_SOURCE_DIR}/src/leveldb/include
        ${CMAKE_SOURCE_DIR}/src/univalue/include
        ${CMAKE_SOURCE_DIR}/src/secp256k1/include
        ${CMAKE_SOURCE_DIR}/src/chiabls/src
        ${relic_SOURCE_DIR}/include
        ${relic_BINARY_DIR}/include
        ${CMAKE_CURRENT_SOURCE_DIR}
        ${CMAKE_CURRENT_SOURCE_DIR}/lats
        ${CMAKE_CURRENT_SOURCE_DIR}/lats/settings
        ${BerkeleyDB_INCLUDE_DIRS}
        )
set_property(TARGET qt_stuff PROPERTY CXX_STANDARD 14)

file(GLOB QT_TRANSLATIONS_FILES ${CMAKE_CURRENT_SOURCE_DIR}/locale/*.ts)

get_filename_component(QM_FILES_BINARY_DIR "${CMAKE_CURRENT_SOURCE_DIR}/locale" ABSOLUTE)
set_source_files_properties(${QT_TRANSLATIONS_FILES} PROPERTIES OUTPUT_LOCATION "${QM_FILES_BINARY_DIR}")

QT5_ADD_TRANSLATION(QM ${QT_TRANSLATIONS_FILES})
add_custom_target(translations_target ALL DEPENDS ${QM})

QT5_ADD_RESOURCES(QRC_RESOURCE lats.qrc)
QT5_ADD_RESOURCES(QRC_LOCALE_RESOURCE lats_locale.qrc)

add_executable(lats-qt lats.cpp ${QM} ${QRC_RESOURCE} ${QRC_LOCALE_RESOURCE})
add_dependencies(lats-qt translations_target libunivalue libsecp256k1 libzcashrust leveldb crc32c bls)
target_include_directories(lats-qt PUBLIC ${ENDIAN_INCLUDES} ${GMP_INCLUDE_DIR})
target_link_libraries(lats-qt
        qt_stuff
        univalue
        SERVER_A WALLET_A COMMON_A ZEROCOIN_A UTIL_A SAPLING_A BITCOIN_CRYPTO_A CLI_A
        leveldb crc32c secp256k1 rustzcash bls
        ${BerkeleyDB_LIBRARIES} ${Boost_LIBRARIES} ${LIBEVENT_LIB}
        ${sodium_LIBRARY_RELEASE} ${GMP_LIBRARY}
        -ldl pthread
        )
if (${CMAKE_SYSTEM_NAME} MATCHES "Darwin")
    target_link_libraries(lats-qt "-framework Cocoa")
endif()
if(ZMQ_FOUND)
    target_link_libraries(lats-qt ZMQ_A ${ZMQ_LIB})
    target_include_directories(lats-qt PUBLIC ${ZMQ_INCLUDE_DIR})
endif()
if (QRCODE_FOUND)
    target_link_libraries(lats-qt ${QRCODE_LIB})
    target_include_directories(lats-qt PUBLIC ${QRCODE_INCLUDE_DIR})
endif()
if(MINIUPNP_FOUND)
    target_compile_definitions(lats-qt PUBLIC "-DSTATICLIB -DMINIUPNP_STATICLIB")
    target_link_libraries(lats-qt ${MINIUPNP_LIBRARY})
    target_include_directories(lats-qt PUBLIC ${MINIUPNP_INCLUDE_DIR})
endif()
if(NAT-PMP_FOUND)
    target_link_libraries(lats-qt ${NAT-PMP_LIBRARY})
    target_include_directories(lats-qt PUBLIC ${NAT-PMP_INCLUDE_DIR})
endif()

target_link_libraries(lats-qt Qt5::Gui Qt5::Core Qt5::Widgets Qt5::Network Qt5::Svg ${QT_LIBRARIES})
if (Qt5DBus_FOUND)
    target_link_libraries(lats-qt Qt5::DBus ${QT_LIBRARIES})
endif()
if (Qt5Charts_FOUND)
    target_link_libraries(lats-qt Qt5::Charts ${QT_LIBRARIES})
endif()
