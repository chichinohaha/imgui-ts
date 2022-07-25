# Imgui-ts

## 背景

Emscripten is a complete Open Source compiler toolchain to WebAssembly.

JavaScript bindings for Dear ImGui using Emscripten and TypeScript, modularized with webpack for imgui-js

[原生的 imgui Github 地址](https://www.npmjs.com/package/@zhobo63/imgui-ts)
[npm imgui-ts 地址](https://www.npmjs.com/package/@zhobo63/imgui-ts)
[Emscripten](https://emscripten.org/docs/introducing_emscripten/about_emscripten.html)

## 核心部分简单示例

[Dear ImGui](https://github.com/ocornut/imgui/blob/master/docs/README.md)
[ImGui JavaScript+WebGL+Webpack example](https://zhobo63.github.io/imgui-ts/)

### Hover 样式

``` c++
    if (ImGui::TreeNode("Mouse cursors"))
    {
        const char* mouse_cursors_names[] = { "Arrow", "TextInput", "ResizeAll", "ResizeNS", "ResizeEW", "ResizeNESW", "ResizeNWSE", "Hand", "NotAllowed" };
        IM_ASSERT(IM_ARRAYSIZE(mouse_cursors_names) == ImGuiMouseCursor_COUNT);

        ImGuiMouseCursor current = ImGui::GetMouseCursor();
        ImGui::Text("Current mouse cursor = %d: %s", current, mouse_cursors_names[current]);
        ImGui::Text("Hover to see mouse cursors:");
        ImGui::SameLine(); HelpMarker(
            "Your application can render a different mouse cursor based on what ImGui::GetMouseCursor() returns. "
            "If software cursor rendering (io.MouseDrawCursor) is set ImGui will draw the right cursor for you, "
            "otherwise your backend needs to handle it.");
        for (int i = 0; i < ImGuiMouseCursor_COUNT; i++)
        {
            char label[32];
            sprintf(label, "Mouse cursor %d: %s", i, mouse_cursors_names[i]);
            ImGui::Bullet(); ImGui::Selectable(label, false);
            if (ImGui::IsItemHovered())
                ImGui::SetMouseCursor(i);
        }
        ImGui::TreePop();
    }
```

### 文本输入与布局

```ts
// 画布中新增 Hello 面板
ImGui.Begin("Hello");
// 展示文本
ImGui.Text("Version " + ImGui.VERSION);
// 双向绑定文本以及右侧显示 Input 
ImGui.InputText("Input", this.text);
// 设置下一行的文案的宽度为沾满一行
ImGui.SetNextItemWidth(-ImGui.FLT_MIN);
ImGui.InputText("Input2", this.text2);
// 指定输入框的长度以及文案样式为密码框
ImGui.InputText("Password", this.text, this.text.size, ImGui.InputTextFlags.Password);
ImGui.InputTextMultiline("Text", this.text_area);
ImGui.SetNextItemWidth(-ImGui.FLT_MIN);
ImGui.InputTextMultiline("Text2", this.text_area2);
// 使用滚动条展示向量的四个变量并双向绑定以及在右侧显示 Slider
ImGui.SliderFloat4("Slider", this.v4, 0,100);
// 使用输入框展示向量的四个变量并双向绑定以及在右侧显示 Float
ImGui.InputFloat4("Float4", this.v4);

ImGui.End();
ImGui.EndFrame();
ImGui.Render();
ImGui_Impl.ClearBuffer(new ImGui.ImVec4(0.25, 0.25, 0.25, 1));
ImGui_Impl.RenderDrawData(ImGui.GetDrawData());
```

## 如何在编辑器内复刻该功能

todo
