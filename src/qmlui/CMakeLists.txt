# Builds the qtui module

#set(QT_DONT_USE_QTGUI 0)
#set(QT_USE_QTDECLARATIVE 1)
#include(${QT_USE_FILE})


set(SOURCES
#    qmlchatline.cpp
    qmlchatview.cpp
    qmlmessagemodel.cpp
    qmlmessagemodelitem.cpp
)

set(MOC_HDRS
#    qmlchatline.h
    qmlchatview.h
    qmlmessagemodel.h
)

set(HEADERS
    qmlmessagemodelitem.h
)

set(FORMS

)

foreach(FORM ${FORMS})
  set(FORMPATH ${FORMPATH} ui/${FORM})
endforeach(FORM ${FORMS})

qt_wrap_cpp(MOC ${MOC_HDRS} ${SPHDR})
qt_wrap_ui(UI ${FORMPATH} ${SPFRM})

include_directories(${CMAKE_SOURCE_DIR}/src/common
                    ${CMAKE_SOURCE_DIR}/src/client
                    ${CMAKE_SOURCE_DIR}/src/uisupport
                    ${CMAKE_CURRENT_BINARY_DIR})

set(CLIENT_RCS ${CLIENT_RCS} qmlui/qml/qml.qrc PARENT_SCOPE)

add_library(mod_qmlui STATIC ${SOURCES} ${SPSRC} ${MOC} ${DBUS} ${UI} ${HEADERS})
qt_use_modules(mod_qmlui Core QuickWidgets Network ${QT_MODULES})
target_link_libraries(mod_qmlui mod_client mod_common mod_uisupport ${LIBS})
#add_dependencies(mod_qmlui mod_common mod_client mod_uisupport)
