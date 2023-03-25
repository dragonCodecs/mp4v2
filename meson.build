project(
	'MP4v2',
	'cpp',
	default_options: [
		'buildtype=release',
		'strip=true',
		'b_lto=true',
		'cpp_std=c++11'
	],
	license: 'LGPL2',
	version: '2.1.2',
)

cxx = meson.get_compiler('cpp')
if target_machine.system() == 'windows'
	add_project_arguments('-D_CRT_SECURE_NO_WARNINGS', language: 'cpp')
endif

libraryDefs = ['-DHAVE_CONFIG_H']
if target_machine.system() == 'windows'
	if get_option('default_library') == 'static'
		libraryDefs += ['-DMP4V2_USE_STATIC_LIB']
	else
		libraryDefs += ['-DMP4V2_EXPORTS']
	endif
endif

m = cxx.find_library('m', required: false)

subdir('libplatform')
subdir('include/mp4v2')

mp4v2Srcs = files(
	'libplatform/io/File.cpp', 'libplatform/io/FileSystem.cpp', 'libplatform/prog/option.cpp',
	'libplatform/sys/error.cpp', 'libplatform/time/time.cpp',
	'libutil/TrackModifier.cpp', 'libutil/Utility.cpp', 'libutil/other.cpp',
	'src/3gp.cpp', 'src/atom_ac3.cpp', 'src/atom_amr.cpp', 'src/atom_avc1.cpp', 'src/atom_avcC.cpp',
	'src/atom_chpl.cpp', 'src/atom_colr.cpp', 'src/atom_d263.cpp', 'src/atom_dac3.cpp', 'src/atom_damr.cpp',
	'src/atom_dref.cpp', 'src/atom_elst.cpp', 'src/atom_enca.cpp', 'src/atom_encv.cpp', 'src/atom_free.cpp',
	'src/atom_ftab.cpp', 'src/atom_ftyp.cpp', 'src/atom_gmin.cpp', 'src/atom_hdlr.cpp', 'src/atom_hinf.cpp',
	'src/atom_hnti.cpp', 'src/atom_href.cpp', 'src/atom_mdat.cpp', 'src/atom_mdhd.cpp', 'src/atom_meta.cpp',
	'src/atom_mp4s.cpp', 'src/atom_mp4v.cpp', 'src/atom_mvhd.cpp', 'src/atom_nmhd.cpp', 'src/atom_ohdr.cpp',
	'src/atom_pasp.cpp', 'src/atom_root.cpp', 'src/atom_rtp.cpp', 'src/atom_s263.cpp', 'src/atom_sdp.cpp',
	'src/atom_sdtp.cpp', 'src/atom_smi.cpp', 'src/atom_sound.cpp', 'src/atom_standard.cpp', 'src/atom_stbl.cpp',
	'src/atom_stdp.cpp', 'src/atom_stsc.cpp', 'src/atom_stsd.cpp', 'src/atom_stsz.cpp', 'src/atom_stz2.cpp',
	'src/atom_text.cpp', 'src/atom_tfhd.cpp', 'src/atom_tkhd.cpp', 'src/atom_treftype.cpp', 'src/atom_trun.cpp',
	'src/atom_tx3g.cpp', 'src/atom_udta.cpp', 'src/atom_url.cpp', 'src/atom_urn.cpp', 'src/atom_uuid.cpp',
	'src/atom_video.cpp', 'src/atom_vmhd.cpp', 'src/cmeta.cpp', 'src/descriptors.cpp', 'src/exception.cpp',
	'src/isma.cpp', 'src/log.cpp', 'src/mp4.cpp', 'src/mp4atom.cpp', 'src/mp4container.cpp', 'src/mp4descriptor.cpp',
	'src/mp4file.cpp', 'src/mp4file_io.cpp', 'src/mp4info.cpp', 'src/mp4property.cpp',
	'src/mp4track.cpp', 'src/mp4util.cpp', 'src/ocidescriptors.cpp', 'src/odcommands.cpp', 'src/qosqualifiers.cpp',
	'src/rtphint.cpp', 'src/text.cpp', 'src/bmff/typebmff.cpp', 'src/itmf/CoverArtBox.cpp', 'src/itmf/Tags.cpp',
	'src/itmf/generic.cpp', 'src/itmf/type.cpp', 'src/qtff/ColorParameterBox.cpp', 'src/qtff/PictureAspectRatioBox.cpp',
	'src/qtff/coding.cpp'
)

if target_machine.system() == 'windows'
	mp4v2Srcs += [
		'libplatform/io/FileSystem_win32.cpp', 'libplatform/io/File_win32.cpp',
		'libplatform/number/random_win32.cpp',
		'libplatform/time/time_win32.cpp', 'libplatform/platform_win32.cpp',
	]
else
	mp4v2Srcs += [
		'libplatform/io/FileSystem_posix.cpp', 'libplatform/io/File_posix.cpp',
		'libplatform/number/random_posix.cpp',
		'libplatform/time/time_posix.cpp',
	]
endif

libmp4v2_includes = include_directories('.', 'include')

if get_option('default_library') == 'static'
	libmp4v2 = static_library(
		'mp4v2',
		mp4v2Srcs,
		include_directories: libmp4v2_includes,
		cpp_args: libraryDefs,
		dependencies: m,
		gnu_symbol_visibility: 'inlineshidden',
	)
else
	libmp4v2 = shared_library(
		'mp4v2',
		mp4v2Srcs,
		include_directories: libmp4v2_includes,
		cpp_args: libraryDefs,
		dependencies: m,
		gnu_symbol_visibility: 'inlineshidden',
		version: meson.project_version()
	)
endif

mp4v2_dep = declare_dependency(
	link_with: libmp4v2,
	dependencies: m,
	include_directories: libmp4v2_includes,
)

meson.override_dependency('mp4v2', mp4v2_dep)

subdir('libutil')

utils = [
	'mp4art', 'mp4chaps', 'mp4extract', 'mp4file', 'mp4info', 'mp4subtitle', 'mp4track', 'mp4trackdump'
]

foreach utility : utils
	executable(
		utility,
		'util/@0@.cpp'.format(utility),
		include_directories: include_directories('include'),
		link_with: [libmp4v2, libutil],
		gnu_symbol_visibility: 'inlineshidden',
		install: true,
	)
endforeach

pkg = import('pkgconfig')

pkg.generate(
	libmp4v2,
	description: 'A library for manipulating MP4 container files'
)
