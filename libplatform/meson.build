config = configuration_data()

config.set('HAVE_DLFCN_H', cxx.has_header('dlfcn.h'))
config.set('HAVE_INTTYPES_H', cxx.has_header('inttypes.h'))
config.set('HAVE_MEMORY_H', cxx.has_header('memory.h'))
config.set('HAVE_STDINT_H', cxx.has_header('stdint.h'))
config.set('HAVE_STDLIB_H', cxx.has_header('stdlib.h'))
config.set('HAVE_STRINGS_H', cxx.has_header('strings.h'))
config.set('HAVE_STRING_H', cxx.has_header('string.h'))
config.set('HAVE_SYS_STAT_H', cxx.has_header('sys/stat.h'))
config.set('HAVE_SYS_TYPES_H', cxx.has_header('sys/types.h'))
config.set('HAVE_UNISTD_H', cxx.has_header('unistd.h'))

config.set('PACKAGE', meson.project_name().to_lower())
config.set('PACKAGE_BUGREPORT', '')
config.set('PACKAGE_NAME', meson.project_name())
config.set('PACKAGE_STRING', '@0@ @1@'.format(meson.project_name(), meson.project_version()))
config.set('PACKAGE_TARNAME', meson.project_name().to_lower())
config.set('PACKAGE_VERSION', meson.project_version())
config.set('VERSION', meson.project_version())

config.set('PROJECT_email', '')
config.set('PROJECT_name', meson.project_name())
config.set('PROJECT_name_formal', meson.project_name())
config.set('PROJECT_name_lower', meson.project_name().to_lower())
config.set('PROJECT_url_website', '')
config.set('PROJECT_version', meson.project_version())

configure_file(
	input: 'config.h.cmake',
	output: 'config.h',
	configuration: config,
	format: 'cmake@'
)
