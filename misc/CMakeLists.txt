project(cctools_misc)

# To avoid name conflicts with tools from cctools-port
FUNCTION(add_cctools_misc exe)
	add_darling_executable(${exe}_cctools_misc ${exe}.c)
	target_link_libraries(${exe}_cctools_misc libstuff)
	set_target_properties(${exe}_cctools_misc
		PROPERTIES OUTPUT_NAME ${exe})
	install(TARGETS ${exe}_cctools_misc
		DESTINATION ${CCTOOLS_INSTALL_DEST})
ENDFUNCTION(add_cctools_misc)

add_cctools_misc(lipo)
add_cctools_misc(strings)
add_cctools_misc(size)
add_cctools_misc(checksyms)
add_cctools_misc(indr)
add_cctools_misc(strip)
add_cctools_misc(segedit)
add_cctools_misc(cmpdylib)
add_cctools_misc(pagestuff)
add_cctools_misc(redo_prebinding)
add_cctools_misc(seg_addr_table)
add_cctools_misc(check_dylib)
add_cctools_misc(seg_hack)
add_cctools_misc(install_name_tool)
# Genuine signer helper (not a signer): the Security.framework signer invokes
# this through CODESIGN_ALLOCATE or its /usr/bin default and fails with
# errSecCSHelperFailed if it is absent. Install it under the canonical cctools
# destination with a declared component so a prefix can receive only the
# signing helper without a full cctools deploy.
add_darling_executable(codesign_allocate_cctools_misc codesign_allocate.c)
target_link_libraries(codesign_allocate_cctools_misc libstuff)
set_target_properties(codesign_allocate_cctools_misc PROPERTIES OUTPUT_NAME codesign_allocate)
install(TARGETS codesign_allocate_cctools_misc
	DESTINATION ${CCTOOLS_INSTALL_DEST}
	COMPONENT codesign_allocate)
add_cctools_misc(ctf_insert)
add_cctools_misc(bitcode_strip)
add_cctools_misc(nm)

add_cctools_misc(libtool)

# vtool is different (no libstuff)
add_darling_executable(vtool_cctools_misc vtool.c)
set_target_properties(vtool_cctools_misc PROPERTIES OUTPUT_NAME vtool)
install(TARGETS vtool_cctools_misc DESTINATION ${CCTOOLS_INSTALL_DEST})

# TODO: nmedit -- strip with -DNMEDIT
# TODO: libredo_prebinding
