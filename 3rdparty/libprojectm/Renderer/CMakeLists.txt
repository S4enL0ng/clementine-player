PROJECT(Renderer)
cmake_minimum_required(VERSION 3.10.0)

if(COMMAND cmake_policy)
  cmake_policy(SET CMP0003 NEW)
endif(COMMAND cmake_policy)

SET(SOIL_SOURCES SOIL/image_DXT.c SOIL/image_helper.c SOIL/SOIL.c SOIL/stb_image_aug.c)

SET(Renderer_SOURCES FBO.cpp MilkdropWaveform.cpp PerPixelMesh.cpp Pipeline.cpp Renderer.cpp  ShaderEngine.cpp UserTexture.cpp  Waveform.cpp 
Filters.cpp PerlinNoise.cpp PipelineContext.cpp  Renderable.cpp BeatDetect.cpp Shader.cpp TextureManager.cpp VideoEcho.cpp 
RenderItemDistanceMetric.cpp RenderItemMatcher.cpp ${SOIL_SOURCES})

if(MSVC)
	SET (MATH_LIBRARIES )
else(MSVC)
	SET (MATH_LIBRARIES m)
endif(MSVC)

FIND_PACKAGE(X11)

INCLUDE_DIRECTORIES(${projectM_SOURCE_DIR} ${X11_INCLUDE_DIR})
ADD_LIBRARY(Renderer STATIC ${Renderer_SOURCES})
SET_TARGET_PROPERTIES(Renderer PROPERTIES VERSION 2.00 SOVERSION 2)
TARGET_LINK_LIBRARIES(Renderer ${MATH_LIBRARIES} ${GLEW_LIBRARIES} projectM)

set_target_properties(Renderer PROPERTIES COMPILE_FLAGS "-Wno-parentheses")
