cmake_minimum_required(VERSION 3.22)

project(SFZ2DS VERSION 1.1.0)

include(FetchContent)
FetchContent_Declare(
    JUCE
    GIT_REPOSITORY https://github.com/juce-framework/JUCE.git
    GIT_TAG 8.0.12
    GIT_SHALLOW TRUE
)
FetchContent_MakeAvailable(JUCE)

juce_add_console_app(SFZ2DS
    PRODUCT_NAME "SFZ2DS"
    COMPANY_NAME "David Hilowitz"
    COMPANY_WEBSITE "http://decided.ly"
    COMPANY_EMAIL "dhilowitz@gmail.com"
    BUNDLE_ID "ly.decided.SFZ2DS"
)

juce_generate_juce_header(SFZ2DS)

target_sources(SFZ2DS PRIVATE
    Source/Main.cpp
    Source/DSPresetConverter/Source/DSPresetConverter.cpp
    Source/DSPresetConverter/Source/DSEXS24.cpp
    Source/DSPresetConverter/Source/DSSFZ.cpp
)

target_compile_definitions(SFZ2DS PRIVATE
    JUCE_DISABLE_JUCE_VERSION_PRINTING=1
    JUCE_STRICT_REFCOUNTEDPOINTER=1
    JUCE_WEB_BROWSER=0
    JUCE_USE_CURL=0
)

target_link_libraries(SFZ2DS PRIVATE
    juce::juce_audio_basics
    juce::juce_audio_devices
    juce::juce_audio_formats
    juce::juce_core
    juce::juce_cryptography
    juce::juce_data_structures
    juce::juce_events
    juce::juce_recommended_config_flags
    juce::juce_recommended_lto_flags
    juce::juce_recommended_warning_flags
)
