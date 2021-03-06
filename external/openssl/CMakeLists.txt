project(android-external-openssl)

if( WINDOWS )
	include_directories(../../../../../dependencies/windows/dlfcn/include)
endif() 

# Defines from android-config.mk
add_definitions(-DOPENSSL_THREADS -D_REENTRANT -DL_ENDIAN)
add_definitions(-DOPENSSL_NO_CAMELLIA -DOPENSSL_NO_CAPIENG -DOPENSSL_NO_CAST -DOPENSSL_NO_CMS -DOPENSSL_NO_GMP -DOPENSSL_NO_IDEA -DOPENSSL_NO_JPAKE -DOPENSSL_NO_MD2 -DOPENSSL_NO_MDC2 -DOPENSSL_NO_RC5 -DOPENSSL_NO_SHA0 -DOPENSSL_NO_RFC3779 -DOPENSSL_NO_SEED -DOPENSSL_NO_STORE -DOPENSSL_NO_WHIRLPOOL)
add_definitions(-DOPENSSL_NO_STATIC_ENGINE -DOPENSSL_NO_GOST-DOPENSSL_NO_DTLS1 -DOPENSSL_NO_RSAX -DOPENSSL_NO_RDRAND )
# Carl DZLIB is not defined in the new file
# add_definitions( -DZLIB )
if( WINDOWS )
else()
	add_definitions(-DDSO_DLFCN -DHAVE_DLFCN_H )
endif()
# New symbols 
add_definitions(-DMONOLITH)
add_definitions(-DOPENSSL_NO_EC_NISTP_64_GCC_128 -DOPENSSL_NO_HEARTBEATS -DOPENSSL_NO_SCTP -DTERMIO )

add_subdirectory(crypto)
add_subdirectory(ssl)
set(EXTERNAL_OPENSSL_OBJECTS
  ${EXTERNAL_OPENSSL_CRYPTO_OBJECTS}
  ${EXTERNAL_OPENSSL_SSL_OBJECTS}
  PARENT_SCOPE
)

