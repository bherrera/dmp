#/*******************************************************************************
# * Copyright (c) 2012- Fundação CERTI
# * All rights reserved.
# *******************************************************************************/

cmake_minimum_required(VERSION 2.8)
project(CERTI_CommonLibs)

set(CMAKE_MODULE_PATH ${PROJECT_SOURCE_DIR}/build)
include(CertiCommonLibs)

IF(NOT CERTI_THIRD_PARTY_BUILD)
  add_subdirectory(dev)
ELSE(NOT CERTI_THIRD_PARTY_BUILD)
  execute_process(COMMAND /bin/bash -c "if [ ! -d ${CERTI_PREBUILT_DIR} ]; then mkdir ${CERTI_PREBUILT_DIR}; fi")
  execute_process(COMMAND /bin/bash -c "if [ ! -d ${CERTI_PREBUILT_USR_DIR} ]; then mkdir ${CERTI_PREBUILT_USR_DIR}; fi")

  add_custom_target(third-party ALL
	COMMAND make -C ${CERTI_COMMON_LIBS_ROOT_DIR}/tools/buildroot-2012.02 O=${CERTI_PREBUILT_USR_DIR} ${CERTI_PRODUCT_PLAT}_defconfig 
	COMMAND make BOARDDIR=./board/${CERTI_PRODUCT_MANUFACTOR}/${CERTI_PRODUCT_BOARD_NAME}
	COMMAND cd staging && cd `pwd -P` && cd .. && tar -jcvf ${CERTI_PREBUILT_USR_DIR}/sysroot.tar.bz2 ./sysroot > /dev/null
	COMMAND cd host && cd `pwd -P` && cd .. && tar -jcvf ${CERTI_PREBUILT_USR_DIR}/host.tar.bz2 ./host > /dev/null
	  WORKING_DIRECTORY ${CERTI_PREBUILT_USR_DIR}
  )

  SET(CERTI_BUILDROOT_CONFIG_FILE ${CERTI_COMMON_LIBS_ROOT_DIR}/tools/buildroot-2012.02/.config)
  add_custom_target(menuconfig
	COMMAND cp ${CERTI_COMMON_LIBS_ROOT_DIR}/tools/buildroot-2012.02/configs/${CERTI_PRODUCT_PLAT}_defconfig ${CERTI_BUILDROOT_CONFIG_FILE}
	COMMAND make -C ${CERTI_COMMON_LIBS_ROOT_DIR}/tools/buildroot-2012.02 menuconfig
  COMMAND make -C ${CERTI_COMMON_LIBS_ROOT_DIR}/tools/buildroot-2012.02 savedefconfig
	COMMAND cp ${CERTI_COMMON_LIBS_ROOT_DIR}/tools/buildroot-2012.02/defconfig ${CERTI_COMMON_LIBS_ROOT_DIR}/tools/buildroot-2012.02/configs/${CERTI_PRODUCT_PLAT}_defconfig
  )

  add_custom_target(deploy
	COMMAND cp ${CERTI_PREBUILT_USR_DIR}/sysroot.tar.bz2 ${CERTI_PREBUILT_DIR}
	COMMAND cp ${CERTI_PREBUILT_USR_DIR}/host.tar.bz2 ${CERTI_PREBUILT_DIR}
	COMMAND cp ${CERTI_PREBUILT_USR_DIR}/images/rootfs.tar.bz2 ${CERTI_PREBUILT_DIR}
  )
ENDIF(NOT CERTI_THIRD_PARTY_BUILD)

set(CERTI_SSH_CLIENT $ENV{SSH_CLIENT})
IF(DEFINED CERTI_SSH_CLIENT)
  set(CERTI_REMOTE_DIR "/tmp/${CERTI_PRODUCT_PLAT}")
  set(CERTI_REMOTE_USER $ENV{REMOTE_USER})
  string (REGEX MATCH "[0-9]+.[0-9]+.[0-9]+.[0-9]+" CERTI_REMOTE_IP $ENV{SSH_CLIENT})
  add_custom_target(transfer
  	echo "${CERTI_REMOTE_USER}@${CERTI_REMOTE_IP}:${CERTI_REMOTE_DIR}"
  	COMMAND rsync -avzh --rsync-path=\"mkdir -p ${CERTI_REMOTE_DIR} && rsync\" ${CERTI_BUILD_OUTPUT_ROOT_DIR} ${CERTI_REMOTE_USER}@${CERTI_REMOTE_IP}:${CERTI_REMOTE_DIR}
  	WORKING_DIRECTORY ${CERTI_COMMON_LIBS_ROOT_DIR})
ENDIF(DEFINED CERTI_SSH_CLIENT)

