[![Build status](https://ci.appveyor.com/api/projects/status/j09x8n07u3byfky0?svg=true)](https://ci.appveyor.com/project/LukasBanana/llgl)

Low Level Graphics Library (LLGL)
=================================

<p align="center"><img src="docu/LLGL_Logo.png"/></p>

License
-------

[3-Clause BSD License](https://github.com/LukasBanana/LLGL/blob/master/LICENSE.txt)


Documentation
-------------

- [Getting Started with LLGL](https://github.com/LukasBanana/LLGL/blob/master/docu/GettingStarted/Getting%20Started%20with%20LLGL.pdf) (PDF)
with Introduction, Hello Triangle Tutorial, and Extensibility Example with [GLFW](http://www.glfw.org/)
- [LLGL Reference Manual](https://github.com/LukasBanana/LLGL/blob/master/docu/refman.pdf) (PDF)
- [LLGL Coding Conventions](https://github.com/LukasBanana/LLGL/blob/master/docu/CodingConventions/Coding%20Conventions%20for%20LLGL.pdf) (PDF)


Progress
--------

* **Version**: 0.02 Beta (see [ChangeLog](docu/ChangeLog))

| Renderer | Progress | Remarks |
|----------|:--------:|---------|
| OpenGL | ~90% | |
| Direct3D 11 | ~85% | Depth-textures are incomplete |
| Direct3D 12 | ~15% | Experimental state; Tutorials working: 01, (02), (03), 06, 07, (10) |
| Vulkan | ~30% | Experimental state; Tutorials working: 01, 02, 03, 06, 07, 10 |

| Platform | Progress | Remarks |
|----------|:--------:|---------|
| Windows | 100% | Tested on *Windows 10* |
| Linux | 50% | Tested on *Kubuntu 16*; Anti-aliasing is currently not supported |
| macOS | 50% | Tested on *macOS Sierra*; Not all tutorials are running |
| iOS | 1% | Currently not compilable |


Thin Abstraction Layer
----------------------

```cpp
// Unified Interface:
CommandBuffer::DrawIndexed(std::uint32_t numIndices, std::uint32_t firstIndex);

// OpenGL Implementation:
void GLCommandBuffer::DrawIndexed(std::uint32_t numIndices, std::uint32_t firstIndex)
{
    const GLsizeiptr indices = firstIndex * renderState_.indexBufferStride;
    glDrawElements(
        renderState_.drawMode,
        static_cast<GLsizei>(numIndices),
        renderState_.indexBufferDataType,
        reinterpret_cast<const GLvoid*>(indices)
    );
}

// Direct3D 11 Implementation
void D3D11CommandBuffer::DrawIndexed(std::uint32_t numIndices, std::uint32_t firstIndex)
{
    context_->DrawIndexed(numIndices, firstIndex, 0);
}

// Direct3D 12 Implementation
void D3D12CommandBuffer::DrawIndexed(std::uint32_t numIndices, std::uint32_t firstIndex)
{
    commandList_->DrawIndexedInstanced(numIndices, 1, firstIndex, 0, 0);
}

// Vulkan Implementation
void VKCommandBuffer::DrawIndexed(std::uint32_t numIndices, std::uint32_t firstIndex)
{
    vkCmdDrawIndexed(commandBuffer_, numIndices, 1, firstIndex, 0, 0);
}
```


Tutorials and Examples
----------------------

This repository contains several tutorials and examples which show how to use LLGL.
Here is a brief overview:

### [Tutorial 01: Hello Triangle](tutorial/Tutorial01_HelloTriangle/main.cpp)

Getting started tutorial where a single multi-colored triangle is rendered.

<p align="center"><img src="tutorial/Tutorial01_HelloTriangle.png" width="400" height="300"/></p>

### [Tutorial 02: Tessellation](tutorial/Tutorial02_Tessellation/main.cpp)

Simple tessellation example without any textures.

<p align="center"><img src="tutorial/Tutorial02_Tessellation.png" width="400" height="300"/></p>

### [Tutorial 03: Texturing](tutorial/Tutorial03_Texturing/main.cpp)

Simple texturing and sampler state example.

<p align="center"><img src="tutorial/Tutorial03_Texturing.png" width="400" height="300"/></p>

### [Tutorial 04: Query](tutorial/Tutorial04_Query/main.cpp)

Shows how to use Query objects and conditional rendering for occlusion culling.

*No screenshot available*

### [Tutorial 05: Render Target](tutorial/Tutorial05_RenderTarget/main.cpp)

Simple render target example with optional multi-sample texture (Texture2DMS/ sampler2DMS).

<p align="center"><img src="tutorial/Tutorial05_RenderTarget.png" width="400" height="300"/></p>

### [Tutorial 06: Multi Context](tutorial/Tutorial06_MultiContext/main.cpp)

Multi-context tutorial shows the following rendering techniques:
multiple render contexts (one window each), rendering simultaneously into multiple viewports, geometry shader.

<p align="center"><img src="tutorial/Tutorial06_MultiContext.png" width="752" height="300"/></p>

### [Tutorial 07: Array](tutorial/Tutorial07_Array/main.cpp)

Shows how to use buffer arrays, i.e. render with multiple vertex buffers simultaneously, and hardware instancing.

<p align="center"><img src="tutorial/Tutorial07_Array.png" width="400" height="300"/></p>

### [Tutorial 08: Compute](tutorial/Tutorial08_Compute/main.cpp)

Small example with a compute shader and a storage buffer.

*No screenshot available*

### [Tutorial 09: StreamOutput](tutorial/Tutorial09_StreamOutput/main.cpp)

Small example with a geometry shader and a stream-output buffer.

*No screenshot available*

### [Tutorial 10: Instancing](tutorial/Tutorial10_Instancing/main.cpp)

Practical example of hardware instancing by rendering tens of thousands of different textured plants instances.

<p align="center"><img src="tutorial/Tutorial10_Instancing.png" width="400" height="300"/></p>

### [Tutorial 11: PostProcessing](tutorial/Tutorial11_PostProcessing/main.cpp)

Practical example of a glow effect with post-processing and the usage of several shaders, render targets and graphics pipelines.

<p align="center"><img src="tutorial/Tutorial11_PostProcessing.png" width="400" height="300"/></p>

### [Tutorial 12: MultiRenderer](tutorial/Tutorial12_MultiRenderer/main.cpp)

Experimental example of using multiple renderers at once (only supported on Win32 platform).

<p align="center"><img src="tutorial/Tutorial12_MultiRenderer.png" width="400" height="300"/></p>



