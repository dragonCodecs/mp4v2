utilSrcs = files(
	'Timecode.cpp', 'crc.cpp',
)

libutil = static_library(
	'util',
	utilSrcs,
	include_directories: libmp4v2_includes,
	gnu_symbol_visibility: 'inlineshidden',
	pic: true
)
