cmake_minimum_required(VERSION 3.15)
project(eqPlugin VERSION 1.0.0)

# Add all dependencies
add_subdirectory(libs)

# `juce_add_plugin` adds a static library target with the name passed as the first argument
# This target is a normal CMake target, but has a lot of extra properties set
# up by default. As well as this shared code static library, this function adds targets for each of
# the formats specified by the FORMATS arguments. This function accepts many optional arguments.
# Check the readme at `docs/CMake API.md` in the JUCE repo for the full list.
juce_add_plugin(eqPlugin
    NEEDS_WEB_BROWSER TRUE
    NEEDS_CURL TRUE
    FORMATS Standalone                  # The formats to build. Other valid formats are: AAX Unity VST AU AUv3
    PRODUCT_NAME "eqPlugin")        # The name of the final executable, which can differ from the target name

target_sources(eqPlugin
    PRIVATE
        apps/GUI/PluginEditor.cpp
        apps/GUI/PluginProcessor.cpp)

target_link_libraries(eqPlugin
    PRIVATE
        juce::juce_audio_utils
    PUBLIC
        juce::juce_recommended_config_flags
        juce::juce_recommended_lto_flags
        juce::juce_recommended_warning_flags)
