ebml_defs = custom_target('ebml_defs.inc',
    output: 'ebml_defs.inc',
    command: [matroska, '--generate-definitions', '@OUTPUT@'],
)

ebml_types = custom_target('ebml_types.h',
    output: 'ebml_types.h',
    command: [matroska, '--generate-header', '@OUTPUT@'],
)

version_h = custom_target('version.h',
    output: 'version.h',
    command: [version_py, '@OUTPUT@'],
    build_always_stale: true,
)

sources += [ebml_defs, ebml_types, version_h]

# Meson doesn't allow having multiple build targets with the same name in the same file.
# Just generate the com in here for windows builds.
if win32 and get_option('cplayer')
    wrapper_sources= '../osdep/win32-console-wrapper.c'
    executable('mpv', wrapper_sources, c_args: '-municode', link_args: '-municode',
               name_suffix: 'com', install: true)
endif
