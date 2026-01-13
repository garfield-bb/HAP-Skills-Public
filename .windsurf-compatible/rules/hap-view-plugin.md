
# HAP 自定义视图插件开发技能

此技能提供创建和开发明道云 HAP 自定义视图插件的完整工作流程和开发规范。

## 关于此技能

此技能专门用于开发明道云 HAP（High-performance Application Platform）自定义视图插件。通过集成的脚手架工具，可以快速创建 React 基础示例模板项目，安装依赖并启动开发环境。

### 🎯 用户反馈规则

**当完成视图插件创建和启动后，只需简洁地告诉用户：**

1. **只显示调试地址**：提供 `http://localhost:3000/bundle.js` 让用户复制到明道云视图配置中
2. **不要展示其他信息**：不需要说明项目结构、常用命令、后续步骤等内容
3. **内部掌握即可**：这些技术细节 AI 自己知道就好，无需向用户展示

**简洁响应示例：**
```
## 🎯 下一步操作

将以下调试地址复制到明道云视图配置的开发调试输入框中：

​```
http://localhost:3000/bundle.js
​```
```

### 🚨 关键行为准则（必须严格遵守）

#### 1. 开发服务器管理

**❌ 禁止行为：**
- 永远不要主动关闭开发服务器（mdye start）
- 不要在用户没有明确要求的情况下执行 Ctrl+C 或 kill 命令
- 不要假设用户已经完成调试而自动关闭服务

**✅ 正确行为：**
- 使用 `run_in_background: true` 启动开发服务器，让它持续运行
- 开发服务器应该一直保持运行状态，直到用户明确要求停止
- 只有当用户说"停止服务器"、"关闭服务"等明确指令时才关闭

**启动服务器的正确方式：**
```bash
# ✅ 正确：后台运行，不会自动关闭
mdye start  # 使用 run_in_background: true

# ❌ 错误：同步运行会阻塞，或者主动关闭
```

#### 2. 构建和发布流程

**❌ 禁止行为：**
- 修改代码后不执行 `mdye build && mdye push`
- 等用户提醒才发布
- 告诉用户"您可以自己发布"

**✅ 正确行为：**
- 每次修改代码后，立即执行 `mdye build && mdye push`
- 主动完成发布，不需要用户额外操作
- 发布成功后明确告知用户"已发布到明道云"

### ⚠️ 关键提醒：每次修改代码后必须重新发布！

**重要行为准则：**

1. **用户每次要求修改代码后**，必须主动执行 `mdye build && mdye push` 发布更新
2. **不要等用户提醒**，这是你的责任！代码修改完成后立即发布
3. **本地开发服务器的热重载只用于预览**，线上环境必须通过 `mdye push` 才能生效
4. **用户说"更新"、"修改"、"添加功能"时**，完成代码修改后，自动执行发布流程

**标准工作流程（每次修改代码）：**
```bash
# 第1步：修改代码（Edit/Write工具）
# 第2步：构建项目
cd <项目目录>
mdye build

# 第3步：提交发布（必须！）
mdye push -m "更新说明：具体修改了什么功能"
```

**错误示例（禁止）：**
- ❌ 修改代码后说"完成了"，但没有执行发布
- ❌ 等用户说"发布"才去执行 mdye push
- ❌ 告诉用户"您可以运行 mdye push 发布"（应该直接帮用户执行）

**正确示例（必须遵守）：**
- ✅ 修改完代码后，立即执行 `mdye build && mdye push`
- ✅ 发布成功后告诉用户"已更新并发布到明道云"
- ✅ 主动完成整个流程，不需要用户额外操作

### 前置条件

在使用此技能前，确保：
1. 已安装 16.20 或更高版本的 Node.js
2. 拥有明道云开发者账号和插件开发权限
3. 了解基本的 React 开发知识

### 开发环境配置

#### Cursor 编辑器配置

下载 `mdye-cursorrules.md` 文件并复制其中内容到视图开发项目根目录下的 `.cursorrules` 文件中，即可在 Cursor 编辑器中获得明道云视图插件开发的智能提示和代码规范检查。

#### 教学 DEMO

请下载明道云视图插件开发教学 DEMO，此插件为开发者提供直观、可交互的 API 使用实例。

### ⚠️ 重要提醒：完整开发流程

**插件开发完成后，必须执行构建和发布步骤！**

完整的开发流程包括：
1. 本地开发（mdye start）
2. **构建项目（mdye build）** ⭐
3. **提交发布（mdye push）** ⭐

**常见错误**：只完成了本地开发和调试，忘记执行 `mdye build` 和 `mdye push` 将插件发布到明道云平台。

**正确做法**：每次开发完成或功能更新后，都需要执行：
```bash
# 1. 构建项目
mdye build

# 2. 提交发布
mdye push -m "功能说明"
```

只有发布后，插件才能在组织内所有应用中使用。详见下方"插件发布流程"章节。

### 核心功能

#### 1. 安装 mdye-cli 工具
- 全局安装插件开发专用的命令行工具
- 验证工具安装是否成功

#### 2. 初始化本地项目
- 创建唯一的插件项目文件夹
- 使用 React 基础示例模板
- 生成项目配置文件

#### 3. 安装项目依赖
- 安装项目所需的 npm 依赖包
- 配置开发环境

#### 4. 启动开发环境
- 启动本地开发服务器
- 支持热重载和实时预览
- 提供线上调试能力

#### 5. 构建和发布（必须！）⭐
- 构建生产版本的 bundle.js
- 提交插件到明道云平台
- 使插件在组织内可用

## 开发工作流程

### 步骤 1：检查并安装 mdye-cli 工具

**首先检查是否已安装：**
```bash
mdye --version
```

如果显示版本号，说明已安装，可以跳过安装步骤。

**如果未安装，根据系统安装：**

**Mac OS 用户：**
```bash
sudo npm install -g mdye-cli
```

**Windows/Linux 用户：**
```bash
npm install -g mdye-cli
```

**验证安装：**
```bash
mdye --version
```

### 步骤 2：初始化本地项目

**创建项目命令：**
```bash
mdye init view --id 693d2fed8474b99be3d3c12e-69563e5df03728c888c04f05 --template React
```

**参数说明：**
- `--id`: 插件 ID（示例 ID，实际使用时需要替换）
- `--template React`: 使用 React 基础示例模板

**项目结构：**
```
mdye_view_69563e5df03728c888c04f05/
├── package.json
├── mdye.json
├── src/
│   ├── index.jsx
│   ├── App.jsx
│   └── styles.less
└── .gitignore
```

### 步骤 3：进入项目目录并安装依赖

**进入项目目录：**
```bash
cd mdye_view_69563e5df03728c888c04f05
```

**安装依赖：**
```bash
npm i
```

### 步骤 4：启动开发环境

**启动命令：**
```bash
mdye start
```

**启动后：**
- 开发服务器将在 `http://localhost:3000/` 启动
- 将调试地址 `http://localhost:3000/bundle.js` 粘贴到明道云视图配置开发调试输入框
- 支持实时编辑和热重载

### 步骤 5：构建和发布插件（必须！）⭐

**⚠️ 重要：开发完成后必须执行此步骤，否则插件无法在组织内使用！**

**构建项目：**
```bash
cd your_plugin_project
mdye build
```

**提交发布：**
```bash
mdye push -m "订单状态视图插件 - 新增产品图片展示功能

功能特性:
- 按订单状态分类展示
- 完整订单信息展示
- 多条关联产品信息展示(含图片)
- 点击订单卡片打开原生行记录弹窗
- 支持编辑/删除订单并自动刷新列表

技术实现:
- 正确处理单选字段(type 9)和关联记录字段(type 29)
- 正确处理附件字段(type 14)解析产品图片
- 使用 utils.openRecordInfo 实现原生交互
- Promise.all 并行加载提升性能"
```

**发布成功标志：**
- 显示 "push成功" 消息
- 返回插件信息和视图地址
- 插件可在组织内所有应用中使用

详细发布流程请参见下方"插件发布流程"章节。

## API 使用指南

### 1. 环境变量及配置获取

#### 1.1 获取 env 环境变量

```javascript
// 使用辅助函数安全获取env中的配置项
function getEnvValue(env, key, defaultValue = null) {
  if (!env || !key) return defaultValue;

  const value = env[key];

  // 处理数组类型(字段选择器)
  if (Array.isArray(value)) {
    return value.length > 0 ? value[0] : defaultValue;
  }

  // 处理普通值
  return value !== undefined ? value : defaultValue;
}

// 使用示例
const titleFieldId = getEnvValue(env, 'title');
const maxRecords = getEnvValue(env, 'maxRecords', '50');
```

#### 1.2 获取 config 配置

```javascript
import { config } from "mdye";

// 获取应用、工作表、视图的ID
const { appId, worksheetId, viewId, controls } = config;

// 获取字段控件信息
const fieldControl = _.find(controls, { controlId: fieldId });
```

### 2. 数据获取 API

#### 2.1 获取工作表数据 (getFilterRows)

```javascript
import { api } from "mdye";

async function loadRecords() {
  const result = await api.getFilterRows({
    worksheetId,     // 必填-工作表ID
    viewId,          // 必填-视图ID
    pageIndex: 1,    // 可选-页码
    pageSize: 50,    // 可选-每页记录数
    sortId: "fieldId", // 可选-排序字段
    isAsc: true,     // 可选-升序排序
    // 获取关联字段数据
    requestParams: {
      plugin_detail_control: relationFieldId
    }
  });

  return result.data; // 记录数组
}
```

#### 2.2 获取记录详情 (getRowDetail)

```javascript
async function getRecordDetail(rowId) {
  const result = await api.getRowDetail({
    appId,
    worksheetId,
    viewId,
    rowId
  });

  return result.data;
}
```

#### 2.3 获取关联记录 (getRowRelationRows)

```javascript
async function loadRelationRows({ controlId, rowId }) {
  const result = await api.getRowRelationRows({
    worksheetId,
    controlId,       // 关联字段ID
    rowId,           // 主记录ID
    pageIndex: 1,
    pageSize: 10
  });

  return result.data;
}
```

### 3. 数据操作 API

#### 3.1 新增记录 (addWorksheetRow)

```javascript
async function addRecord(fieldsData) {
  const response = await api.addWorksheetRow({
    appId,
    worksheetId,
    receiveControls: [
      {
        controlId: "fieldId1",
        type: 2,
        value: "测试文本"
      }
    ]
  });
  return response;
}
```

#### ⚠️ 重要：addWorksheetRow 字段值格式规范

**使用 `addWorksheetRow` 和 `updateWorksheetRow` API 时,不同类型的字段必须使用正确的数据格式,否则会导致保存失败或数据错误。**

##### 1. 关联字段 (type 29) 的正确格式

关联字段必须传递 **包含 `name` 和 `sid` 属性的对象数组的 JSON 字符串**,而不是简单的 ID 数组。

❌ **错误写法:**
```javascript
// 错误:只传递 ID 数组
{
  controlId: "relationFieldId",
  type: 29,
  value: JSON.stringify(["2cd79f0d-9f05-4b63-b3fa-89f661eeb05d"])
}
```

✅ **正确写法:**
```javascript
// 正确:传递包含 name 和 sid 的对象数组
{
  controlId: "relationFieldId",
  type: 29,
  value: JSON.stringify([{
    name: "大连海洋医疗健康发展有限公司",
    sid: "2ccd8ec3-c2c9-4b7c-8331-a4241b2743a0"
  }])
}
```

**单条关联示例:**
```javascript
// 关联客户字段
if (formData.customer) {
  controls.push({
    controlId: '692ed1d0f34d7ea4df717c67',
    type: 29,
    value: JSON.stringify([{
      name: formData.customer.name,  // 必须:记录名称
      sid: formData.customer.sid      // 必须:记录 sid
    }])
  });
}
```

**多条关联示例:**
```javascript
// 关联产品字段(可关联多个产品)
if (formData.products.length > 0) {
  controls.push({
    controlId: '692ed1d0f34d7ea4df717c6e',
    type: 29,
    value: JSON.stringify(formData.products.map(product => ({
      name: product.name,  // 必须:记录名称
      sid: product.sid      // 必须:记录 sid
    })))
  });
}
```

##### 2. 成员字段 (type 26) 的正确格式

成员字段必须传递 **包含 `accountId`、`avatar` 和 `fullname` 属性的对象数组的 JSON 字符串**。

❌ **错误写法:**
```javascript
// 错误:只传递用户 ID 数组
{
  controlId: "ownerFieldId",
  type: 26,
  value: JSON.stringify(["e2453de8-1a6a-4d4f-ba36-87fdff880a20"])
}
```

✅ **正确写法:**
```javascript
// 正确:传递完整的用户对象数组
{
  controlId: "ownerFieldId",
  type: 26,
  value: JSON.stringify([{
    accountId: "e2453de8-1a6a-4d4f-ba36-87fdff880a20",
    avatar: "https://pd.mingdao.com/UserAvatar/e2453de8-1a6a-4d4f-ba36-87fdff880a20.jpg?imageView2/1/w/100/h/100/q/90",
    fullname: "卜佳菲"
  }])
}
```

**完整示例:**
```javascript
// 负责人字段
if (formData.owner) {
  controls.push({
    controlId: '692ed1d0f34d7ea4df717c70',
    type: 26,
    value: JSON.stringify([{
      accountId: formData.owner.accountId,  // 必须:用户账号 ID
      avatar: formData.owner.avatar,        // 必须:用户头像 URL
      fullname: formData.owner.fullname     // 必须:用户全名
    }])
  });
}
```

##### 3. 子表字段 (type 34) 的正确格式

子表字段也需要传递 **包含完整字段结构的对象数组的 JSON 字符串**,每个子表行记录是一个对象,包含该行的所有字段值。

**子表字段数据结构:**
```javascript
// 子表字段格式
{
  controlId: "subtableFieldId",
  type: 34,
  value: JSON.stringify([
    {
      // 第一行记录
      "fieldId1": "值1",
      "fieldId2": "值2",
      // ... 其他字段
    },
    {
      // 第二行记录
      "fieldId1": "值3",
      "fieldId2": "值4",
      // ... 其他字段
    }
  ])
}
```

**完整示例 - 订单明细子表:**
```javascript
// 假设订单明细子表包含:产品、数量、单价、小计等字段
if (formData.orderDetails && formData.orderDetails.length > 0) {
  controls.push({
    controlId: '692ed1d0f34d7ea4df717c6f', // 订单明细子表字段ID
    type: 34,
    value: JSON.stringify(formData.orderDetails.map(detail => ({
      // 子表中的产品关联字段(type 29)
      '692ed1d0f34d7ea4df717c80': JSON.stringify([{
        name: detail.product.name,
        sid: detail.product.sid
      }]),
      // 子表中的数量字段(type 6)
      '692ed1d0f34d7ea4df717c81': detail.quantity,
      // 子表中的单价字段(type 6)
      '692ed1d0f34d7ea4df717c82': detail.price,
      // 子表中的小计字段(type 31 公式字段,通常不需要传值)
      // '692ed1d0f34d7ea4df717c83': detail.subtotal
    })))
  });
}
```

**注意事项:**
1. 子表中的关联字段仍然需要使用 `{name, sid}` 格式
2. 子表中的成员字段仍然需要使用 `{accountId, avatar, fullname}` 格式
3. 公式字段、汇总字段等自动计算的字段通常不需要传值
4. 子表字段值是 **双重 JSON 字符串**:外层是整个子表数组,内层的关联字段等也需要 JSON.stringify

##### 3. 表单数据结构设计建议

为了正确使用 API,建议在表单数据结构中直接存储完整的对象信息:

```javascript
// ✅ 推荐的 formData 结构
const [formData, setFormData] = useState({
  orderNumber: '',
  customer: null,    // 存储完整对象 {name, sid, rowid}
  contact: null,     // 存储完整对象 {name, sid, rowid}
  products: [],      // 存储完整对象数组 [{name, sid, rowid}, ...]
  owner: null,       // 存储完整对象 {accountId, avatar, fullname}
  // 其他字段...
});

// ❌ 不推荐:只存储 ID
const [formData, setFormData] = useState({
  orderNumber: '',
  customerId: '',     // 只有 ID,调用 API 时还需要查找 name
  contactId: '',      // 只有 ID,调用 API 时还需要查找 name
  productIds: [],     // 只有 ID 数组,调用 API 时还需要查找 name
  ownerId: '',        // 只有 ID,调用 API 时还需要查找 fullname 和 avatar
  // 其他字段...
});
```

##### 4. 使用 utils.selectRecord 和 utils.selectUsers 获取完整对象

在选择记录或用户时,应存储完整的对象信息:

```javascript
// 选择关联记录
const handleSelectCustomer = async () => {
  try {
    // 获取关联字段的 dataSource (目标工作表 ID)
    const customerControl = controls?.find(ctrl => ctrl.controlId === 'customerFieldId');

    const records = await utils.selectRecord({
      projectId: appId,
      relateSheetId: customerControl?.dataSource,  // ✅ 使用 dataSource,不要硬编码
      multiple: false
    });

    if (records && records.length > 0) {
      const record = records[0];
      // ✅ 存储完整的记录对象信息
      setFormData(prev => ({
        ...prev,
        customer: {
          name: record.name || record.title || '',
          sid: record.sid || record.rowid,
          rowid: record.rowid
        }
      }));
    }
  } catch (error) {
    console.error('选择客户失败:', error);
  }
};

// 选择成员
const handleSelectOwner = async () => {
  try {
    const users = await utils.selectUsers({
      projectId: appId,
      unique: true  // 单选
    });

    if (users && users.length > 0) {
      const user = users[0];
      // ✅ 存储完整的用户对象信息
      setFormData(prev => ({
        ...prev,
        owner: {
          accountId: user.accountId,
          avatar: user.avatar || '',
          fullname: user.fullname || user.name || ''
        }
      }));
    }
  } catch (error) {
    console.error('选择负责人失败:', error);
  }
};
```

##### 4.1 自定义选择界面的样式设计指南

当使用 `utils.selectRecord` 和 `utils.selectUsers` 时,需要设计用户友好的选择按钮界面。

**选择前的样式（空状态）:**

```javascript
// styled-components 示例
const SelectButton = styled.button`
  width: 100%;
  padding: 10px 12px;
  border: 1px solid #ddd;
  border-radius: 6px;
  font-size: 14px;
  background: #fff;
  cursor: pointer;
  text-align: left;
  transition: all 0.3s;
  color: #999; // 空状态使用灰色文本

  &:hover {
    border-color: #2196f3;
    background: #f5f9ff;
  }

  &:active {
    transform: scale(0.98);
  }

  // 空状态占位符样式
  &.empty {
    color: #999;
  }

  // 已选择状态
  &.selected {
    color: #333;
    font-weight: 500;
  }
`;

// React 组件使用示例
<div className="form-group">
  <label>客户</label>
  <SelectButton
    onClick={handleSelectCustomer}
    className={formData.customer ? 'selected' : 'empty'}
  >
    {formData.customer ? formData.customer.name : '选择客户'}
  </SelectButton>
</div>
```

**选择后的样式（已选择状态）:**

```javascript
// 显示已选择项的完整信息
<div className="form-group">
  <label>负责人</label>
  <SelectButton
    onClick={handleSelectOwner}
    className={formData.owner ? 'selected' : 'empty'}
  >
    {formData.owner ? (
      <div style={{ display: 'flex', alignItems: 'center', gap: '8px' }}>
        {/* 可选:显示用户头像 */}
        {formData.owner.avatar && (
          <img
            src={formData.owner.avatar}
            alt={formData.owner.fullname}
            style={{ width: '24px', height: '24px', borderRadius: '50%' }}
          />
        )}
        <span>{formData.owner.fullname}</span>
        {/* 可选:添加清除按钮 */}
        <span
          onClick={(e) => {
            e.stopPropagation();
            setFormData(prev => ({ ...prev, owner: null }));
          }}
          style={{ marginLeft: 'auto', color: '#999', cursor: 'pointer' }}
        >
          ×
        </span>
      </div>
    ) : (
      '选择负责人'
    )}
  </SelectButton>
</div>
```

**多选字段的展示示例:**

```javascript
<div className="form-group">
  <label>关联产品</label>
  <SelectButton
    onClick={handleSelectProducts}
    className={formData.products.length > 0 ? 'selected' : 'empty'}
  >
    {formData.products.length > 0 ? (
      <div>
        <div style={{ fontWeight: '500', marginBottom: '4px' }}>
          已选择 {formData.products.length} 个产品
        </div>
        <div style={{ fontSize: '12px', color: '#666' }}>
          {formData.products.map(p => p.name).join(', ')}
        </div>
      </div>
    ) : (
      '选择产品'
    )}
  </SelectButton>
</div>
```

**完整的样式示例（使用 styled-components）:**

```javascript
const SelectButton = styled.button`
  width: 100%;
  padding: 10px 12px;
  border: 1px solid #ddd;
  border-radius: 6px;
  font-size: 14px;
  background: #fff;
  cursor: pointer;
  text-align: left;
  transition: all 0.3s;
  color: #333;

  &:hover {
    border-color: #2196f3;
    background: #f5f9ff;
  }

  &:active {
    transform: scale(0.98);
  }

  // 空状态样式
  &.empty {
    color: #999;

    &::after {
      content: '▼';
      float: right;
      color: #ccc;
    }
  }

  // 已选择状态样式
  &.selected {
    border-color: #2196f3;
    background: #f5f9ff;

    .selected-info {
      display: flex;
      align-items: center;
      gap: 8px;

      .avatar {
        width: 24px;
        height: 24px;
        border-radius: 50%;
        object-fit: cover;
      }

      .name {
        flex: 1;
        font-weight: 500;
        color: #333;
      }

      .clear-btn {
        margin-left: auto;
        color: #999;
        font-size: 18px;
        padding: 0 4px;
        transition: color 0.2s;

        &:hover {
          color: #f44336;
        }
      }
    }
  }
`;
```

**最佳实践建议:**

1. **视觉反馈清晰**: 使用不同的颜色、字体粗细区分空状态和已选择状态
2. **显示选中内容**: 选择后显示实际的名称,而不是"已选择"这样的模糊文本
3. **支持快速清除**: 为已选择项提供清除按钮,无需重新打开选择对话框
4. **多选计数提示**: 多选字段显示已选择的数量和简要列表
5. **交互动画**: 使用过渡动画提升用户体验
6. **响应式设计**: 确保在不同屏幕尺寸下都有良好的显示效果

##### 5. 完整的创建记录示例

```javascript
async function handleSubmitCreate() {
  try {
    // 验证必填字段
    if (!formData.orderNumber) {
      alert('请输入订单编号');
      return;
    }

    // 构建字段数据
    const controls = [
      // 文本字段
      {
        controlId: '692ed1d0f34d7ea4df717c66',
        type: 2,
        value: formData.orderNumber
      }
    ];

    // 单条关联字段 - 客户
    if (formData.customer) {
      controls.push({
        controlId: '692ed1d0f34d7ea4df717c67',
        type: 29,
        value: JSON.stringify([{
          name: formData.customer.name,
          sid: formData.customer.sid
        }])
      });
    }

    // 单条关联字段 - 联系人
    if (formData.contact) {
      controls.push({
        controlId: '692ed1d0f34d7ea4df717c69',
        type: 29,
        value: JSON.stringify([{
          name: formData.contact.name,
          sid: formData.contact.sid
        }])
      });
    }

    // 日期字段
    if (formData.orderDate) {
      controls.push({
        controlId: '692ed1d0f34d7ea4df717c6b',
        type: 15,
        value: formData.orderDate
      });
    }

    // 数值字段
    if (formData.amount) {
      controls.push({
        controlId: '692ed1d0f34d7ea4df717c6c',
        type: 6,
        value: formData.amount
      });
    }

    // 单选字段
    if (formData.status) {
      controls.push({
        controlId: '692ed1d0f34d7ea4df717c6d',
        type: 9,
        value: JSON.stringify([formData.status])
      });
    }

    // 多条关联字段 - 产品
    if (formData.products.length > 0) {
      controls.push({
        controlId: '692ed1d0f34d7ea4df717c6e',
        type: 29,
        value: JSON.stringify(formData.products.map(product => ({
          name: product.name,
          sid: product.sid
        })))
      });
    }

    // 成员字段 - 负责人
    if (formData.owner) {
      controls.push({
        controlId: '692ed1d0f34d7ea4df717c70',
        type: 26,
        value: JSON.stringify([{
          accountId: formData.owner.accountId,
          avatar: formData.owner.avatar,
          fullname: formData.owner.fullname
        }])
      });
    }

    // 文本字段 - 备注
    if (formData.notes) {
      controls.push({
        controlId: '692ed1d0f34d7ea4df717c71',
        type: 2,
        value: formData.notes
      });
    }

    // 调用创建记录 API
    const result = await api.addWorksheetRow({
      appId,
      worksheetId,
      receiveControls: controls
    });

    if (result && result.data) {
      console.log('订单创建成功:', result.data);
      // 关闭弹窗并刷新列表
      setShowCreateDialog(false);
      loadOrders();
    }
  } catch (error) {
    console.error('创建订单失败:', error);
    alert('创建订单失败: ' + error.message);
  }
}
```

##### 6. 常见错误及排查

**错误1: 关联字段保存失败或保存后为空**
- 原因: 只传递了 ID,未传递 `{name, sid}` 对象
- 解决: 确保传递完整的对象结构

**错误2: 成员字段保存失败或显示异常**
- 原因: 只传递了 accountId,未传递 `{accountId, avatar, fullname}` 对象
- 解决: 确保传递完整的用户对象

**错误3: utils.selectRecord 获取不到记录**
- 原因: 使用了硬编码的 worksheetId 而非字段配置中的 dataSource
- 解决: 从关联字段控件的 `dataSource` 属性获取正确的工作表 ID

**调试技巧:**
```javascript
// 在调用 API 前,打印完整的 controls 数组
console.log('准备创建记录,字段数据:', JSON.stringify(controls, null, 2));

// 检查关联字段配置
const customerControl = controls?.find(ctrl => ctrl.controlId === 'customerFieldId');
console.log('客户关联字段配置:', customerControl);
console.log('目标工作表 ID:', customerControl?.dataSource);

// 检查选择的记录结构
console.log('选中的客户记录:', record);
console.log('提取的数据:', {
  name: record.name || record.title,
  sid: record.sid || record.rowid
});
```

#### 3.2 更新记录 (updateWorksheetRow)

```javascript
async function updateRecord(rowId, fieldId, newValue) {
  const response = await api.updateWorksheetRow({
    appId,
    worksheetId,
    rowId,
    newOldControl: [
      {
        controlId: fieldId,
        type: 2,
        value: newValue
      }
    ]
  });
  return response;
}
```

#### 3.3 删除记录 (deleteWorksheetRow)

```javascript
async function deleteRecord(rowId) {
  const response = await api.deleteWorksheetRow({
    appId,
    worksheetId,
    rowIds: [rowId]
  });
  return response;
}
```

### 4. 工具函数 (utils)

#### 4.1 打开记录详情（推荐使用！）

**使用 `utils.openRecordInfo` 打开明道云原生行记录组件是最佳实践:**

优势:
- ✅ 原生体验,与明道云界面一致
- ✅ 功能完整:支持编辑、删除、讨论、日志、附件等所有功能
- ✅ 自动处理权限验证
- ✅ 无需自己开发弹窗 UI
- ✅ 返回操作结果,方便进行数据同步

**基础用法:**

```javascript
import { utils } from "mdye";

// 打开记录详情
const handleRecordClick = async (recordId) => {
  try {
    const result = await utils.openRecordInfo({
      appId,
      worksheetId,
      viewId,
      recordId
    });

    // 处理返回结果
    if (result) {
      console.log('操作结果:', result);

      // 根据操作类型处理
      switch (result.action) {
        case 'update':
          // 记录被更新,刷新数据
          console.log('记录已更新:', result.value);
          loadRecords(); // 重新加载数据
          break;
        case 'delete':
          // 记录被删除,刷新列表
          console.log('记录已删除');
          loadRecords(); // 重新加载数据
          break;
        case 'close':
          // 用户关闭弹窗(无修改)
          console.log('用户关闭了弹窗');
          break;
      }
    }
  } catch (error) {
    console.error('打开记录详情失败:', error);
  }
};
```

**返回值说明:**

```javascript
{
  action: 'update' | 'delete' | 'close',  // 操作类型
  value: object | null                     // 更新后的记录数据(仅 action='update' 时)
}
```

**完整的 React Hook 示例(包含自动刷新):**

```javascript
import React, { useEffect, useState } from 'react';
import { config, api, utils } from 'mdye';

function RecordsList() {
  const { appId, worksheetId, viewId } = config;
  const [records, setRecords] = useState([]);
  const [loading, setLoading] = useState(false);

  // 加载记录列表
  const loadRecords = async () => {
    try {
      setLoading(true);
      const result = await api.getFilterRows({
        worksheetId,
        viewId,
        pageSize: 100,
        pageIndex: 1
      });
      setRecords(result.data || []);
    } catch (error) {
      console.error('加载记录失败:', error);
    } finally {
      setLoading(false);
    }
  };

  // 打开记录详情
  const handleRecordClick = async (recordId) => {
    try {
      const result = await utils.openRecordInfo({
        appId,
        worksheetId,
        viewId,
        recordId
      });

      // 自动刷新列表
      if (result?.action === 'update' || result?.action === 'delete') {
        loadRecords(); // 刷新数据
      }
    } catch (error) {
      console.error('打开记录详情失败:', error);
    }
  };

  // 初始加载
  useEffect(() => {
    loadRecords();
  }, []);

  return (
    <div>
      {loading ? (
        <div>加载中...</div>
      ) : (
        <div>
          {records.map(record => (
            <div
              key={record.rowid}
              onClick={() => handleRecordClick(record.rowid)}
              style={{ cursor: 'pointer' }}
            >
              {record.title}
            </div>
          ))}
        </div>
      )}
    </div>
  );
}
```

**性能优化建议:**

```javascript
// 1. 使用 useCallback 避免重复创建函数
const handleRecordClick = useCallback(async (recordId) => {
  const result = await utils.openRecordInfo({
    appId, worksheetId, viewId, recordId
  });
  if (result?.action === 'update' || result?.action === 'delete') {
    loadRecords();
  }
}, [appId, worksheetId, viewId]);

// 2. 只在需要时刷新
const handleRecordClick = async (recordId) => {
  const result = await utils.openRecordInfo({
    appId, worksheetId, viewId, recordId
  });

  // 根据具体操作决定是否刷新
  if (result?.action === 'update') {
    // 局部更新(性能更好)
    setRecords(prev =>
      prev.map(r => r.rowid === recordId ? result.value : r)
    );
  } else if (result?.action === 'delete') {
    // 从列表中移除
    setRecords(prev => prev.filter(r => r.rowid !== recordId));
  }
};
```

#### 4.2 打开新建记录窗口

```javascript
utils.openNewRecord({
  appId,
  worksheetId
}).then(newRecord => {
  if (newRecord) {
    addLocalRecord(newRecord);
  }
});
```

#### 4.3 选择用户

```javascript
const users = await utils.selectUsers({
  projectId: "orgId1",
  unique: false  // 是否单选
});
```

#### 4.4 选择部门

```javascript
const departments = await utils.selectDepartments({
  projectId: "orgId1",
  unique: false
});
```

#### 4.5 选择位置

```javascript
const location = await utils.selectLocation({
  distance: 1000,
  defaultPosition: { lat: 39.915, lng: 116.404 },
  multiple: false
});
```

#### 4.6 选择记录

```javascript
const records = await utils.selectRecord({
  projectId: "orgId1",
  relateSheetId: "worksheetId1",
  multiple: true
});
```

### 5. 事件监听

#### 5.1 筛选条件变更事件

```javascript
import { md_emitter } from "mdye";

useEffect(() => {
  const handleFiltersUpdate = (newFilters) => {
    console.log('筛选条件已更新:', newFilters);
    // 重新获取数据
  };

  md_emitter.addListener('filters-update', handleFiltersUpdate);

  return () => {
    md_emitter.removeListener('filters-update', handleFiltersUpdate);
  };
}, []);
```

#### 5.2 新增记录事件

```javascript
useEffect(() => {
  const handleNewRecord = (newRecord) => {
    console.log('新增记录:', newRecord);
    setRecords(prev => [...prev, newRecord]);
  };

  md_emitter.addListener('new-record', handleNewRecord);

  return () => {
    md_emitter.removeListener('new-record', handleNewRecord);
  };
}, []);
```

## 特殊字段类型处理

### ⚠️ 重要提示:字段类型编号

**明道云字段类型编号与文档中的枚举值不完全一致,开发时务必注意:**

根据明道云 API V3 版本的实际字段类型定义:
- **Type 9** = 单选 (SingleSelect) ⚠️ 注意不是 type 11
- **Type 10** = 多选 (MultipleSelect)
- **Type 11** = 下拉 (Dropdown)

### 完整字段类型对照表(V3 实用版)

| 类型编号 | 枚举名称 | 字段类型 | API 创建 | API 返回 |
|---------|---------|---------|---------|---------|
| 2 | Text | 文本框 | ✅ | ✅ |
| 3 | PhoneNumber | 手机 | ❌ | ✅ |
| 4 | LandlinePhone | 座机 | ❌ | ✅ |
| 5 | Email | 邮箱 | ❌ | ✅ |
| 6 | Number | 数值 | ✅ | ✅ |
| 7 | Certificate | 证件 | ❌ | ✅ |
| 8 | Currency | 金额 | ❌ | ✅ |
| **9** | **SingleSelect** | **单选** | ✅ | ✅ |
| 10 | MultipleSelect | 多选 | ✅ | ✅ |
| 11 | Dropdown | 下拉 | ❌ | ✅ |
| 14 | Attachment | 附件 | ✅ | ✅ |
| 15 | Date | 日期 | ✅ | ✅ |
| 16 | DateTime | 时间 | ✅ | ✅ |
| 19/23/24 | Region | 地区 | ❌ | ✅ |
| 21 | DynamicLink | 自由链接 | ❌ | ✅ |
| 22 | Divider | 分段 | ❌ | ❌ |
| 25 | AmountInWords | 大写金额 | ❌ | ✅ |
| 26 | Collaborator | 成员 | ✅ | ✅ |
| 27 | Department | 部门 | ❌ | ✅ |
| 28 | Rating | 等级 | ❌ | ✅ |
| 29 | Relation | 连接他表 | ✅ | ✅ |
| 30 | Lookup | 他表字段 | ❌ | ✅ |
| 31 | Formula | 公式 | ❌ | ✅ |
| 32 | Concatenate | 文本拼接 | ❌ | ✅ |
| 33 | AutoNumber | 自动编号 | ❌ | ✅ |
| 34 | SubTable | 子表 | ❌ | ✅ |
| 35 | CascadingSelect | 级联选择 | ❌ | ✅ |
| 36 | Checkbox | 检查框 | ❌ | ✅ |
| 37 | Rollup | 汇总 | ❌ | ✅ |
| 38 | DateFormula | 公式(日期) | ❌ | ✅ |
| 39 | CodeScan | 扫码 | ❌ | ✅ |
| 40 | Location | 定位 | ❌ | ✅ |
| 41 | RichText | 富文本 | ❌ | ✅ |
| 42 | Signature | 签名 | ❌ | ✅ |
| 43 | OCR | 文字识别 | ❌ | ✅ |
| 44 | Role | 角色 | ❌ | ✅ |
| 45 | Embed | 嵌入 | ❌ | ❌ |
| 46 | Time | 时间 | ✅ | ✅ |
| 47 | Barcode | 条码 | ❌ | ✅ |
| 48 | OrgRole | 组织角色 | ❌ | ✅ |

### 常见错误示例

❌ **错误写法:**
```javascript
// 只查找 type 10 和 11,会遗漏 type 9 的单选字段
const selectField = controls?.find(ctrl =>
  ctrl.controlName?.includes('状态') && (ctrl.type === 10 || ctrl.type === 11)
);
```

✅ **正确写法:**
```javascript
// 包含 type 9, 10, 11 所有选项字段类型
const selectField = controls?.find(ctrl =>
  ctrl.controlName?.includes('状态') && (ctrl.type === 9 || ctrl.type === 10 || ctrl.type === 11)
);
```

### 字段解析函数

#### 单选字段

```javascript
function parseSingleSelect(value, control) {
  try {
    if (!value) return { key: "", text: "" };

    const keys = typeof value === 'string'
      ? JSON.parse(value)
      : (Array.isArray(value) ? value : []);

    const selectedKey = keys[0] || "";

    let selectedText = "";
    if (control && control.options) {
      const option = control.options.find(opt => opt.key === selectedKey);
      selectedText = option ? option.value : "";
    }

    return { key: selectedKey, text: selectedText };
  } catch (err) {
    console.error("解析单选字段失败:", err);
    return { key: "", text: "" };
  }
}
```

#### 多选字段

```javascript
function parseMultiSelect(value, control) {
  try {
    if (!value) return [];

    const keys = typeof value === 'string'
      ? JSON.parse(value)
      : (Array.isArray(value) ? value : []);

    const result = [];
    if (control && control.options) {
      keys.forEach(key => {
        const option = control.options.find(opt => opt.key === key);
        if (option) {
          result.push({ key: key, text: option.value });
        }
      });
    }

    return result;
  } catch (err) {
    console.error("解析多选字段失败:", err);
    return [];
  }
}
```

#### 成员字段

```javascript
function parseMembers(value) {
  try {
    if (!value) return [];
    return typeof value === 'string' ? JSON.parse(value) : value;
  } catch (err) {
    return [];
  }
}
```

#### 附件字段

```javascript
function parseAttachments(value) {
  try {
    if (!value) return [];
    return typeof value === 'string' ? JSON.parse(value) : value;
  } catch (err) {
    return [];
  }
}
```

#### 定位字段

```javascript
function parseLocation(value) {
  try {
    if (!value) return { title: "", address: "", x: 0, y: 0 };
    return typeof value === 'string' ? JSON.parse(value) : value;
  } catch (err) {
    return { title: "", address: "", x: 0, y: 0 };
  }
}
```

#### 关联记录字段（⚠️ 重要！）

**关联字段 (type 29) 的特殊处理规则:**

关联字段根据 `enumDefault` 或 `subType` 属性分为两种类型,返回数据格式完全不同:

1. **单条关联** (enumDefault=1 或 subType=1)
   - 返回格式: JSON 数组字符串
   - 示例: `"[{\"sid\":\"...\",\"name\":\"客户名称\",\"sourcevalue\":\"...\"}]"`
   - 处理方式: 直接解析 JSON 字符串即可

2. **多条关联** (enumDefault=2 或 subType=2)
   - 返回格式: 数字(表示关联记录的数量)
   - 示例: `2` (表示关联了 2 条记录)
   - 处理方式: **必须调用 `getRowRelationRows` API** 才能获取实际数据

**完整处理示例:**

```javascript
// 1. 判断是否为多条关联
function isMultipleRelation(value) {
  return typeof value === 'number' || (!isNaN(value) && value !== '');
}

// 2. 解析单条关联数据
function parseRelationData(value) {
  try {
    if (!value) return [];

    const relations = typeof value === 'string' ? JSON.parse(value) : value;
    if (!Array.isArray(relations)) return [];

    return relations.map(item => {
      let sourceValue = {};
      if (item.sourcevalue) {
        try {
          sourceValue = typeof item.sourcevalue === 'string'
            ? JSON.parse(item.sourcevalue)
            : item.sourcevalue;
        } catch (e) {
          console.error("解析sourcevalue失败:", e);
        }
      }

      return {
        sid: item.sid || '',
        name: item.name || '',
        rowid: sourceValue.rowid || '',
        ...item
      };
    });
  } catch (err) {
    console.error("解析关联记录字段失败:", err);
    return [];
  }
}

// 3. 完整使用示例（包含单条和多条处理）
async function loadOrdersWithProducts() {
  const result = await api.getFilterRows({
    worksheetId,
    viewId,
    pageSize: 1000,
    pageIndex: 1
  });

  // 使用 Promise.all 并行处理所有订单
  const ordersData = await Promise.all(
    result.data.map(async (row) => {
      // 获取关联产品字段值
      const productsValue = row['relationFieldId'];
      let products = [];

      // 判断是单条还是多条关联
      if (isMultipleRelation(productsValue)) {
        // 多条关联:调用 API 获取详情
        try {
          const relationResult = await api.getRowRelationRows({
            worksheetId,
            controlId: 'relationFieldId',  // 关联字段ID
            rowId: row.rowid,
            pageSize: 100,
            pageIndex: 1
          });

          if (relationResult && relationResult.data) {
            products = relationResult.data.map(item => ({
              name: item['productNameFieldId'],    // 产品名称字段ID
              code: item['productCodeFieldId'],    // 产品编码字段ID
              price: item['productPriceFieldId'],  // 产品单价字段ID
              rowid: item.rowid
            }));
          }
        } catch (error) {
          console.error('获取多条关联失败:', error);
        }
      } else {
        // 单条关联:直接解析
        products = parseRelationData(productsValue);
      }

      return {
        id: row.rowid,
        products: products,
        productsCount: isMultipleRelation(productsValue)
          ? Number(productsValue)
          : products.length
      };
    })
  );

  return ordersData;
}
```

**字段配置示例:**

```javascript
// 在 config.controls 中查看关联字段配置
const relationControl = controls.find(ctrl => ctrl.controlId === 'relationFieldId');

// 单条关联配置
{
  "controlId": "692ed1d0f34d7ea4df717c67",
  "type": 29,
  "controlName": "关联客户",
  "enumDefault": 1,  // 或 subType: 1
  // ... 其他属性
}

// 多条关联配置
{
  "controlId": "692ed1d0f34d7ea4df717c6e",
  "type": 29,
  "controlName": "关联产品",
  "enumDefault": 2,  // 或 subType: 2
  // ... 其他属性
}
```

### 自动获取字段值的工具函数

```javascript
function getFieldValue(fieldId, record, controls) {
  if (!fieldId || !record) return null;

  const rawValue = record[fieldId];
  if (rawValue === undefined) return null;

  const control = controls.find(ctrl => ctrl.controlId === fieldId);
  if (!control) return rawValue;

  const fieldType = getFieldTypeByControlType(control.type);

  switch (fieldType) {
    case 'text':
    case 'email':
    case 'phone':
      return rawValue;

    case 'number':
      return parseFloat(rawValue) || 0;

    case 'select':
      return parseSingleSelect(rawValue, control);

    case 'multiselect':
      return parseMultiSelect(rawValue, control);

    case 'user':
      return parseMembers(rawValue);

    case 'department':
      return parseDepartments(rawValue);

    case 'attachment':
      return parseAttachments(rawValue);

    case 'location':
      return parseLocation(rawValue);

    case 'boolean':
      return rawValue === "1" || rawValue === 1 || rawValue === true;

    case 'relation':
      return parseRelationData(rawValue);

    default:
      return rawValue;
  }
}

function getFieldTypeByControlType(controlType) {
  const typeMap = {
    2: 'text',           // 文本框
    3: 'phone',          // 手机
    4: 'phone',          // 座机
    5: 'email',          // 邮箱
    6: 'number',         // 数值
    7: 'certificate',    // 证件
    8: 'number',         // 金额
    9: 'select',         // 单选 ⚠️ 重要:type 9 是单选
    10: 'multiselect',   // 多选
    11: 'select',        // 下拉
    14: 'attachment',    // 附件
    15: 'date',          // 日期
    16: 'datetime',      // 时间
    19: 'region',        // 地区
    23: 'region',        // 地区
    24: 'region',        // 地区
    26: 'user',          // 成员
    27: 'department',    // 部门
    28: 'rating',        // 等级
    29: 'relation',      // 连接他表
    36: 'boolean',       // 检查框
    40: 'location',      // 定位
    41: 'richtext',      // 富文本
    42: 'signature',     // 签名
    46: 'time',          // 时间
    48: 'role',          // 组织角色
  };
  return typeMap[controlType] || 'unknown';
}
```

## mdye 命令行工具

### 基本命令

```bash
# 查看版本
mdye --version

# 授权登录
mdye auth

# 初始化项目
mdye init view --id <id> --template <template-name>

# 启动开发
mdye start

# 构建项目
mdye build

# 提交插件
mdye push -m "提交说明"

# 查看当前用户
mdye whoami

# 注销
mdye logout

# 同步插件参数配置
mdye sync-params -f <file-path>
```

### 插件发布流程（重要！）

插件开发完成后，需要按以下步骤提交发布到明道云平台。发布成功后，本插件在组织下所有应用均可使用。

#### 第1步：构建项目

执行以下命令将本地项目打包：

```bash
cd your_plugin_project
mdye build
```

**构建过程说明：**
- Webpack 会编译并打包所有源代码
- 生成优化后的 `bundle.js` 文件
- 通常需要 1-2 秒完成编译
- 成功后会显示 "构建代码完成" 和 bundle 文件大小

**构建输出示例：**
```
[21:20:33] 开始构建代码
ℹ Compiling Webpack
✔ Webpack: Compiled successfully in 1.94s
asset bundle.js 228 KiB [emitted] [minimized] (name: main)
webpack 5.98.0 compiled successfully in 1947 ms
[21:20:35] 构建代码完成
```

#### 第2步：提交并发布

执行以下命令将本地项目提交并推送到线上待发布插件列表：

```bash
mdye push -m "提交说明"
```

**提交说明编写建议：**

建议在提交信息中包含以下内容：
1. **功能特性**：列出插件的主要功能
2. **技术实现**：说明关键技术点和优化
3. **版本说明**：首次发布/功能更新/Bug修复

**完整示例：**

```bash
mdye push -m "订单状态视图插件首次发布

功能特性:
- 按订单状态分类展示(待付款/已付款/已发货/已完成/已取消)
- 完整订单信息展示(订单编号/客户/联系人/日期/金额/负责人)
- 多条关联产品信息展示(产品名称/编号/分类/单价)
- 点击订单卡片打开原生行记录弹窗
- 支持编辑/删除订单并自动刷新列表
- 响应式网格布局和流畅动画效果

技术实现:
- 正确处理单选字段(type 9)和关联记录字段(type 29)
- 使用 getRowRelationRows API 处理多条关联
- 使用 utils.openRecordInfo 实现原生交互
- Promise.all 并行加载提升性能"
```

#### 第3步：登录认证

提交时需要登录账户，按提示输入：
- 用户名（手机号或邮箱地址）
- 密码

如果已登录，可以通过 `mdye whoami` 查看当前登录用户。

#### 第4步：确认发布成功

发布成功后会显示插件信息：

```
[21:20:54] 文件上传成功
[21:20:55] push成功
┌──────────────────────────────────────────────────────────┐
│  ---- 插件信息 ----                                       │
│                                                           │
│  插件名称: 自定义视图                                     │
│  视图名称: 自定义视图                                     │
│  视图地址: https://www.mingdao.com/worksheet/...         │
│  提交信息: 订单状态视图插件首次发布                       │
│  提交人: 用户名                                           │
└──────────────────────────────────────────────────────────┘
```

#### 发布后的状态

✅ **插件已发布** - 可以在组织内所有应用中使用
✅ **视图地址** - 可以通过返回的 URL 直接访问插件
✅ **组织共享** - 组织内其他成员可以使用该插件

#### 常见问题

**问题1: 构建失败**
- 检查代码语法错误
- 确保所有依赖已正确安装 (`npm install`)
- 查看错误日志定位问题

**问题2: 推送失败**
- 确认已登录：`mdye whoami`
- 检查网络连接
- 验证账号权限是否支持插件开发

**问题3: 登录超时**
- 重新登录：`mdye auth`
- 输入正确的手机号/邮箱和密码

### 本地项目结构

```
plugin_project/
├── .config/          # 配置文件目录
├── src/              # 源代码目录
│   ├── components/   # 组件目录
│   ├── utils/        # 工具函数目录
│   ├── App.js        # 主应用组件
│   ├── index.js      # 入口文件
│   └── style.less    # 样式文件
├── mdye.json         # 插件配置文件
└── package.json      # 项目依赖配置
```

## 最佳实践

### 1. 项目组织
- 保持项目结构清晰
- 合理划分组件和模块
- 使用有意义的文件命名

### 2. 代码质量
- 遵循 React 最佳实践
- 使用 ESLint 和 Prettier
- 编写清晰的注释和文档

### 3. 性能优化
- 使用 React.memo 优化渲染
- 避免不必要的重渲染
- 优化状态管理
- 使用代码分割

### 4. 安全注意事项
- 避免硬编码敏感信息
- 使用环境变量管理配置
- 验证用户输入
- 防止 XSS 攻击

## 常见问题解决

### 问题 1：选项字段显示 key 而不是文本

**问题描述:** 单选或多选字段显示的是 UUID 格式的 key (如 `42ad38bf-d3e6-441f-a960-670e704abe4a`),而不是选项的显示文本。

**原因分析:**
1. 明道云选项字段返回的原始值是 JSON 格式的 key 数组,如 `"[\"42ad38bf-d3e6-441f-a960-670e704abe4a\"]"`
2. 需要从 `config.controls` 中找到对应字段的 `options`,然后根据 key 匹配出 value

**解决方案:**
```javascript
// 1. 获取字段控件定义(包含options)
const control = config.controls.find(ctrl => ctrl.controlId === fieldId);

// 2. 解析选项字段
function parseSingleSelect(value, control) {
  try {
    if (!value) return { key: "", text: "" };

    // 解析 JSON 字符串得到 key 数组
    let keys = [];
    if (typeof value === 'string') {
      try {
        keys = JSON.parse(value); // ["42ad38bf-..."]
      } catch {
        keys = [value];
      }
    } else if (Array.isArray(value)) {
      keys = value;
    }

    const selectedKey = keys[0] || "";

    // 从 options 中查找对应的显示文本
    let selectedText = "";
    if (control && control.options) {
      const option = control.options.find(opt => opt.key === selectedKey);
      selectedText = option ? option.value : selectedKey;
    }

    return { key: selectedKey, text: selectedText };
  } catch (err) {
    console.error("解析单选字段失败:", err, value);
    return { key: "", text: "" };
  }
}
```

### 问题 2：找不到单选字段

**问题描述:** 使用 `controls.find()` 查找单选字段时,返回 `undefined`。

**原因分析:**
- 单选字段的 type 是 **9** 而不是 11
- type 10 是多选,type 11 是下拉
- 如果只检查 `ctrl.type === 11`,会遗漏 type 9 的单选字段

**解决方案:**
```javascript
// ✅ 正确:包含所有选项字段类型
const selectField = controls?.find(ctrl =>
  ctrl.controlName?.includes('状态') &&
  (ctrl.type === 9 || ctrl.type === 10 || ctrl.type === 11)
);

// ❌ 错误:会遗漏 type 9
const selectField = controls?.find(ctrl =>
  ctrl.controlName?.includes('状态') &&
  (ctrl.type === 10 || ctrl.type === 11)
);
```

### 问题 3：多条关联字段只显示数字

**问题描述:** 关联字段显示的是数字(如 `2`、`3`),而不是实际的关联记录信息。

**原因分析:**
1. 多条关联字段 (enumDefault=2 或 subType=2) 返回的原始值是数字,表示关联记录的数量
2. 与单条关联不同,多条关联不会直接返回 JSON 数组字符串
3. 必须调用 `getRowRelationRows` API 才能获取实际的关联记录数据

**解决方案:**

```javascript
// 1. 判断是否为多条关联
function isMultipleRelation(value) {
  return typeof value === 'number' || (!isNaN(value) && value !== '');
}

// 2. 处理关联字段(支持单条和多条)
async function handleRelationField(worksheetId, controlId, rowId, fieldValue) {
  let relationData = [];

  if (isMultipleRelation(fieldValue)) {
    // 多条关联:调用 API 获取详情
    try {
      const result = await api.getRowRelationRows({
        worksheetId,
        controlId,
        rowId,
        pageSize: 100,
        pageIndex: 1
      });

      if (result && result.data) {
        relationData = result.data.map(item => ({
          rowid: item.rowid,
          name: item['titleFieldId'],  // 使用实际的标题字段ID
          // 解析其他需要的字段
        }));
      }
    } catch (error) {
      console.error('获取多条关联失败:', error);
    }
  } else {
    // 单条关联:直接解析
    relationData = parseRelationData(fieldValue);
  }

  return relationData;
}

// 3. 完整使用示例
async function loadRecordsWithRelations() {
  const result = await api.getFilterRows({
    worksheetId,
    viewId,
    pageSize: 100,
    pageIndex: 1
  });

  // 使用 Promise.all 并行处理
  const records = await Promise.all(
    result.data.map(async (row) => {
      const relationValue = row['relationFieldId'];

      const relations = await handleRelationField(
        worksheetId,
        'relationFieldId',
        row.rowid,
        relationValue
      );

      return {
        ...row,
        relations: relations
      };
    })
  );

  return records;
}
```

**如何判断字段是单条还是多条关联:**

```javascript
// 方法1: 查看字段配置
const control = config.controls.find(ctrl => ctrl.controlId === 'relationFieldId');
if (control) {
  const isSingle = control.enumDefault === 1 || control.subType === 1;
  const isMultiple = control.enumDefault === 2 || control.subType === 2;
  console.log('单条关联:', isSingle, '多条关联:', isMultiple);
}

// 方法2: 根据返回值类型判断
const value = row['relationFieldId'];
if (typeof value === 'number' || !isNaN(value)) {
  console.log('这是多条关联,需要调用 getRowRelationRows');
} else if (typeof value === 'string') {
  console.log('这是单条关联,可以直接解析 JSON');
}
```

### 问题 4：npm 安装失败
- 检查网络连接
- 清理 npm 缓存：`npm cache clean --force`
- 使用淘宝镜像：`npm config set registry https://registry.npmmirror.com`

### 问题 2：mdye 命令不存在
- 重新安装 mdye-cli
- 检查 PATH 环境变量
- 使用 `which mdye` 检查安装位置

### 问题 3：项目启动失败
- 检查端口是否被占用
- 检查依赖是否完整安装
- 查看错误日志信息

### 问题 4：插件 ID 冲突
- 使用新的唯一后缀
- 删除旧的冲突项目
- 重新初始化项目

## BI 驾驶舱设计最佳实践

### 什么是 BI 驾驶舱？

BI 驾驶舱（Business Intelligence Dashboard）是从**业务分析师视角**设计的数据可视化界面，而不是简单的数据列表展示。

### BI 驾驶舱 vs 普通视图的区别

**❌ 错误的驾驶舱设计（普通视图思维）：**
- 只显示当前工作表的记录列表
- 简单统计总数、今日新增
- 没有业务逻辑，只是数据展示

**✅ 正确的 BI 驾驶舱设计（分析师思维）：**
- 展示跨表汇总的业务指标
- 显示业务转化漏斗（如销售漏斗）
- 提供多维度趋势分析
- 按业务模块组织数据

### CRM BI 驾驶舱设计案例

以 CRM 应用为例，BI 驾驶舱应该包含：

#### 1. 核心业务指标卡片
```javascript
- 客户总数（包含活跃客户、本月新增）
- 成交机会（总数、已赢单、赢单率）
- 订单金额（总金额、订单数、本月订单）
- 线索转化率（总线索、已转化、转化率）
```

**设计原则：**
- 每个指标卡片包含：主指标 + 辅助指标 + 趋势
- 使用不同颜色的渐变图标区分类别
- 显示同比/环比变化

#### 2. 销售漏斗分析
```javascript
// 展示完整的销售转化流程
线索 → 成交机会 → 报价 → 订单 → 回款

// 可视化方式
- 横向柱状图：展示各阶段数量
- 饼图：展示各阶段占比
- 转化率标注：显示每个阶段的转化率
```

**关键点：**
- 漏斗图必须反映真实的业务流程
- 显示各阶段的转化率和流失率
- 帮助识别业务瓶颈

#### 3. 业务模块统计
```javascript
// 按 CRM 业务模块分类
客户管理模块（👥）
销售管理模块（💰）
产品管理模块（📦）
帐务管理模块（💳）

// 每个模块显示
- 总数
- 今日
- 本周
- 本月
```

**设计原则：**
- 模块划分要符合业务逻辑
- 使用图标快速识别模块类型
- 提供多时间维度统计

#### 4. 业务趋势分析
```javascript
// 30天趋势图
- 面积图：新增 vs 累计
- 折线图：线索 vs 订单
- 柱状图：各产品线对比
```

**可视化选择：**
- 趋势用折线图/面积图
- 对比用柱状图
- 占比用饼图
- 分布用散点图

### 实现 BI 驾驶舱的技术要点

#### 1. 数据获取策略

```javascript
// ❌ 错误：只获取当前工作表
const records = await api.getFilterRows({ worksheetId, viewId });

// ✅ 正确：获取应用结构，跨表汇总
async function loadBIMetrics() {
  // 1. 获取应用结构（通过 MCP 或 API）
  const appInfo = await getAppStructure();

  // 2. 提取所有业务相关的工作表
  const worksheets = extractBusinessWorksheets(appInfo);

  // 3. 并行加载各表数据
  const metricsData = await Promise.all(
    worksheets.map(ws => loadWorksheetMetrics(ws))
  );

  // 4. 汇总计算业务指标
  return calculateBusinessMetrics(metricsData);
}
```

#### 2. 指标计算逻辑

```javascript
// BI 指标应该基于业务逻辑计算
function calculateBusinessMetrics(data) {
  return {
    customers: {
      total: data.customerSheet.total,
      active: data.customerSheet.records.filter(r =>
        r.lastContactDate > thirtyDaysAgo
      ).length,
      newThisMonth: data.customerSheet.records.filter(r =>
        r.ctime >= monthStart
      ).length
    },
    opportunities: {
      total: data.opportunitySheet.total,
      wonCount: data.opportunitySheet.records.filter(r =>
        r.status === '已赢单'
      ).length,
      totalAmount: data.opportunitySheet.records.reduce((sum, r) =>
        sum + (r.amount || 0), 0
      )
    }
    // ... 其他指标
  };
}
```

#### 3. 图表选择指南

| 业务场景 | 推荐图表 | recharts 组件 |
|---------|---------|--------------|
| 销售漏斗 | 横向柱状图 | BarChart (layout="vertical") |
| 转化率 | 饼图 | PieChart |
| 趋势分析 | 面积图/折线图 | AreaChart / LineChart |
| 对比分析 | 柱状图 | BarChart |
| 占比分析 | 饼图/环形图 | PieChart / RadialBarChart |
| 多维分析 | 雷达图 | RadarChart |

#### 4. 响应式布局

```javascript
const Grid = styled.div`
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(280px, 1fr));
  gap: 20px;

  @media (max-width: 768px) {
    grid-template-columns: 1fr;
  }
`;

const ChartCard = styled(Card)`
  grid-column: span 2;  // 图表卡片占两列

  @media (max-width: 768px) {
    grid-column: span 1;  // 移动端占一列
  }
`;
```

### 设计 BI 驾驶舱的思维流程

当用户要求创建 BI 驾驶舱时，按以下步骤思考：

1. **分析业务场景**
   - 这是什么类型的应用？（CRM/ERP/项目管理等）
   - 核心业务流程是什么？
   - 管理层最关心哪些指标？

2. **确定指标维度**
   - 什么是核心 KPI？（客户数、销售额、转化率等）
   - 需要哪些时间维度？（今日/本周/本月/本季度）
   - 需要哪些分类维度？（按产品/按地区/按团队等）

3. **设计数据展示**
   - 顶部：核心 KPI 卡片（4-6个）
   - 中部：业务流程分析（漏斗图、趋势图）
   - 底部：详细模块统计

4. **选择可视化方式**
   - 根据数据类型选择合适的图表
   - 保持视觉一致性（配色、字体、间距）
   - 突出重点数据

### 常见错误及解决方案

#### 错误1：只展示原始数据

**❌ 错误示例：**
```javascript
// 只显示记录列表
<table>
  {records.map(r => <tr><td>{r.name}</td></tr>)}
</table>
```

**✅ 正确示例：**
```javascript
// 计算业务指标后展示
<Card>
  <h3>客户转化率</h3>
  <div className="value">
    {(convertedCount / totalLeads * 100).toFixed(1)}%
  </div>
  <div className="trend">
    较上月 +5.2%
  </div>
</Card>
```

#### 错误2：忽略业务逻辑

**❌ 错误示例：**
```javascript
// 简单统计总数
stats: {
  total: records.length
}
```

**✅ 正确示例：**
```javascript
// 按业务状态分类统计
stats: {
  total: records.length,
  activeCustomers: records.filter(r => isActive(r)).length,
  churnedCustomers: records.filter(r => isChurned(r)).length,
  averageLifetimeValue: calculateLTV(records)
}
```

#### 错误3：图表选择不当

**❌ 错误示例：**
```javascript
// 用饼图展示趋势（错误）
<PieChart data={last30DaysTrend} />
```

**✅ 正确示例：**
```javascript
// 用折线图展示趋势（正确）
<LineChart data={last30DaysTrend}>
  <Line dataKey="newCustomers" stroke="#667eea" />
</LineChart>
```

### 完整的 BI 驾驶舱模板结构

```javascript
export default function BIDashboard() {
  // 1. 状态管理
  const [biMetrics, setBiMetrics] = useState({});
  const [funnel, setFunnel] = useState([]);
  const [trends, setTrends] = useState([]);

  // 2. 数据加载
  useEffect(() => {
    loadBIDashboard();
  }, []);

  async function loadBIDashboard() {
    // 步骤1：获取应用结构
    const appInfo = await getAppStructure();

    // 步骤2：提取工作表
    const worksheets = extractWorksheets(appInfo);

    // 步骤3：计算 BI 指标
    const metrics = await calculateMetrics(worksheets);

    // 步骤4：构建业务分析
    const funnelData = buildSalesFunnel(metrics);
    const trendData = buildTrends(metrics);

    // 步骤5：更新状态
    setBiMetrics(metrics);
    setFunnel(funnelData);
    setTrends(trendData);
  }

  return (
    <DashboardContainer>
      {/* 1. 核心指标 */}
      <Section>
        <KPICards data={biMetrics} />
      </Section>

      {/* 2. 业务漏斗 */}
      <Section>
        <FunnelChart data={funnel} />
      </Section>

      {/* 3. 趋势分析 */}
      <Section>
        <TrendCharts data={trends} />
      </Section>

      {/* 4. 模块统计 */}
      <Section>
        <ModuleStats data={biMetrics.modules} />
      </Section>
    </DashboardContainer>
  );
}
```

### 总结

设计 BI 驾驶舱的核心是：**从业务分析师的视角思考**，而不是从技术视角简单展示数据。

- ✅ 展示业务指标，而不是原始数据
- ✅ 提供业务洞察，而不是数据列表
- ✅ 关注业务流程，而不是单表统计
- ✅ 支持决策分析，而不是查询检索

## 参考资源

- 明道云开发者文档
- React 官方文档
- Node.js 官方文档
- 明道云开发者社区
- Recharts 图表库文档

---

**注意：** 此技能提供的是开发工作流程指导和 API 使用规范，实际开发中请根据具体需求调整配置和代码。
