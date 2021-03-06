cmake_minimum_required(VERSION 2.8)
project("Boids")

set(SRC_FILES
	main.cpp
	../../Chapter8/2_ShadowMaps/Src/Nodes.cpp
	../../Chapter8/2_ShadowMaps/Src/ROP.cpp
	../../Chapter8/2_ShadowMaps/Src/Light.cpp
	../../Chapter8/2_ShadowMaps/Src/Material.cpp
	../../Chapter8/2_ShadowMaps/Src/GLFrameBuffer.cpp
	../../Chapter8/2_ShadowMaps/Src/Loader_OBJ.cpp
	../../Chapter8/2_ShadowMaps/Src/Technique.cpp
	../../Chapter7/1_SDL2UI/Src/Rendering/Canvas.cpp
	../../Chapter7/1_SDL2UI/Src/Rendering/TextRenderer.cpp
	../../Chapter7/1_SDL2UI/Src/SDLWindow.cpp
	../../Chapter7/1_SDL2UI/Src/UI/UIView.cpp
	../../Chapter6/1_GLES3/Engine/Graphics/Bitmap.cpp
	../../Chapter6/1_GLES3/Engine/Graphics/FI_Utils.cpp
	../../Chapter6/1_GLES3/Engine/Core/VecMath.cpp
	../../Chapter6/1_GLES3/Engine/LGL/LGL.cpp
	../../Chapter6/1_GLES3/Engine/LGL/GLClasses.cpp
	../../Chapter5/1_InitOpenAL/Timers.cpp
	../../Chapter4/1_ArchiveFileAccess/src/Archive.cpp
	../../Chapter4/1_ArchiveFileAccess/src/FileSystem.cpp
	../../Chapter4/1_ArchiveFileAccess/src/libcompress.c
	../../Chapter3/2_AsyncTaskQueues/IntrusivePtr.cpp
)

set(HEADER_FILES
	../../Chapter8/2_ShadowMaps/Src/Material.h
	../../Chapter8/2_ShadowMaps/Src/Nodes.h
	../../Chapter8/2_ShadowMaps/Src/ROP.h
	../../Chapter8/2_ShadowMaps/Src/Light.h
	../../Chapter8/2_ShadowMaps/Src/Traversers.h
	../../Chapter8/2_ShadowMaps/Src/GLFrameBuffer.h
	../../Chapter8/2_ShadowMaps/Src/Loader_OBJ.h
	../../Chapter8/2_ShadowMaps/Src/Technique.h
	../../Chapter7/1_SDL2UI/Src/Rendering/Canvas.h
	../../Chapter7/1_SDL2UI/Src/Rendering/TextRenderer.h
	../../Chapter7/1_SDL2UI/Src/SDLWindow.cpp
	../../Chapter7/1_SDL2UI/Src/UI/UIView.cpp
	../../Chapter6/1_GLES3/Engine/Log.h
	../../Chapter6/1_GLES3/Engine/SDLLibrary.h
	../../Chapter6/1_GLES3/Engine/Graphics/Bitmap.h
	../../Chapter6/1_GLES3/Engine/Graphics/FI_Utils.h
	../../Chapter6/1_GLES3/Engine/Graphics/Geometry.cpp
	../../Chapter6/1_GLES3/Engine/Core/VecMath.h
	../../Chapter5/1_InitOpenAL/Timers.h
	../../Chapter4/1_ArchiveFileAccess/src/MountPoint.h
	../../Chapter4/1_ArchiveFileAccess/src/Streams.h
	../../Chapter4/1_ArchiveFileAccess/src/StrUtils.h
	../../Chapter4/1_ArchiveFileAccess/src/Archive.h
	../../Chapter4/1_ArchiveFileAccess/src/FileSystem.h
	../../Chapter4/1_ArchiveFileAccess/src/libcompress.h
	../../Chapter4/1_ArchiveFileAccess/src/Blob.h
	../../Chapter4/1_ArchiveFileAccess/src/Files.h
	../../Chapter3/2_AsyncTaskQueues/IntrusivePtr.h
)

include_directories(
	.
	Src
	../../Chapter8/2_ShadowMaps/Src
	../../Chapter7/1_SDL2UI/Src/
	../../Chapter7/1_SDL2UI/Src/Rendering
	../../Chapter6/1_GLES3
	../../Chapter6/1_GLES3/Engine
	../../Chapter6/1_GLES3/Engine/Core
	../../Chapter6/1_GLES3/Engine/Graphics
	../../Chapter5/1_InitOpenAL
	../../Chapter4/1_ArchiveFileAccess/src
	../../Chapter3/2_AsyncTaskQueues
)

if(NOT MSVC)
	set(CMAKE_CXX_FLAGS "-std=c++11")
endif(NOT MSVC)

add_executable(Boids
	${SRC_FILES}
	${HEADER_FILES}
)

if(MSVC)
	file(COPY SDL2.dll					DESTINATION ./Debug)
	file(COPY freeimage32.dll			DESTINATION ./Debug)
	file(COPY freeimage64.dll			DESTINATION ./Debug)

	find_library(SDL2 NAMES SDL2 PATHS libs.prebuilt ../libs.prebuilt)
	target_link_libraries(Boids
		${SDL2}
	)
endif()
