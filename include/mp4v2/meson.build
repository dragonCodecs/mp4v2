mp4v2_headers = files(
	'chapter.h', 'file.h', 'file_prop.h', 'general.h',
	'isma.h', 'itmf_generic.h', 'itmf_tags.h',
	'mp4v2.h', 'platform.h', 'sample.h',
	'streaming.h', 'track.h', 'track_prop.h',
)

project_h = configure_file(
	input: '../../xcode/include/mp4v2/project.h',
	output: 'project.h',
	copy: true
)

mp4v2_headers += [project_h]

install_headers(
	mp4v2_headers,
	subdir: 'mp4v2'
)
