---
name: word-doc
description: 生成简单的Word文档（.docx），支持表格、标题、段落。当用户说"生成word"、"word文档"、"创建文档"、"导出word"、"生成报告"时触发。使用python-docx库实现，输出到用户桌面。
---

# Word文档生成器

使用python-docx库生成Word文档，输出到用户桌面：`E:\新建文件夹 (4)\`

## 依赖

```bash
pip install python-docx
```

## 生成流程

### 1. 解析用户需求

从用户描述中提取：
- 文档标题
- 表格结构（列数、表头、数据）
- 段落内容
- 其他要求

### 2. 生成Python脚本

创建临时Python脚本 `D:\cc-switch\gen_word.py`，结构如下：

```python
from docx import Document
from docx.shared import Pt, RGBColor
from docx.enum.text import WD_ALIGN_PARAGRAPH
from docx.enum.table import WD_TABLE_ALIGNMENT
from docx.oxml.ns import qn
from docx.oxml import OxmlElement

def set_cell_shading(cell, color):
    """设置单元格背景色"""
    shading = OxmlElement('w:shd')
    shading.set(qn('w:fill'), color)
    shading.set(qn('w:val'), 'clear')
    cell._tc.get_or_add_tcPr().append(shading)

def create_table(doc, headers, rows, header_color="4472C4"):
    """创建格式化表格"""
    table = doc.add_table(rows=len(rows)+1, cols=len(headers))
    table.style = 'Table Grid'
    table.alignment = WD_TABLE_ALIGNMENT.CENTER

    # 表头
    for i, header in enumerate(headers):
        cell = table.rows[0].cells[i]
        cell.text = header
        for paragraph in cell.paragraphs:
            paragraph.alignment = WD_ALIGN_PARAGRAPH.CENTER
            for run in paragraph.runs:
                run.bold = True
                run.font.color.rgb = RGBColor(255, 255, 255)
                run.font.size = Pt(10)
        set_cell_shading(cell, header_color)

    # 数据行（隔行变色）
    for i, row in enumerate(rows):
        for j, cell_text in enumerate(row):
            cell = table.rows[i+1].cells[j]
            cell.text = str(cell_text)
            for paragraph in cell.paragraphs:
                for run in paragraph.runs:
                    run.font.size = Pt(9)
            if i % 2 == 0:
                set_cell_shading(cell, "F2F2F2")

    return table

def main():
    doc = Document()

    # 设置默认字体
    style = doc.styles['Normal']
    style.font.name = '微软雅黑'
    style.font.size = Pt(10)
    style._element.rPr.rFonts.set(qn('w:eastAsia'), '微软雅黑')

    # === 根据用户需求添加内容 ===
    doc.add_heading('文档标题', level=1)
    doc.add_paragraph('正文内容...')

    create_table(doc,
        ['列1', '列2', '列3'],
        [
            ['数据1', '数据2', '数据3'],
            ['数据4', '数据5', '数据6']
        ]
    )

    # 保存到桌面
    output_path = r"E:\新建文件夹 (4)\文档名称.docx"
    doc.save(output_path)
    print(f"已保存: {output_path}")

if __name__ == "__main__":
    main()
```

### 3. 运行脚本

```bash
C:/Users/Lenovo/AppData/Local/Programs/Python/Python313/python.exe D:/cc-switch/gen_word.py
```

### 4. 清理临时文件

```bash
rm D:/cc-switch/gen_word.py
```

### 5. 确认输出

告诉用户文件已生成到桌面。

## 常用组件模板

### 表格
```python
create_table(doc,
    ['姓名', '年龄', '职业'],
    [
        ['张三', '25', '工程师'],
        ['李四', '30', '设计师']
    ]
)
```

### 标题
```python
doc.add_heading('一级标题', level=1)
doc.add_heading('二级标题', level=2)
doc.add_heading('三级标题', level=3)
```

### 段落
```python
doc.add_paragraph('普通段落')

p = doc.add_paragraph()
run = p.add_run('加粗文字')
run.bold = True
```

### 分页
```python
doc.add_page_break()
```

## 注意事项

1. 文件名使用用户指定的名称，如未指定则根据内容自动生成
2. 表格默认蓝色表头+隔行变色
3. 中文字体使用微软雅黑
4. 运行命令使用完整Python路径（Python 3.13）
