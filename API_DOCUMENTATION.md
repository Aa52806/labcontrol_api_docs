# LabControl API 文档

本文档提供了LabControl系统的API详细说明，方便前端开发者使用。

## HTTP请求方法说明

HTTP请求方法（也称为HTTP谓词）是HTTP协议中用于指定对资源执行操作的标准化方法。在LabControl系统中，我们遵循RESTful API设计规范，使用以下HTTP方法：

| 方法 | 名称 | 标准用途 | 在项目中的应用 |
|------|------|----------|----------------|
| GET | 获取 | 检索资源或资源列表 | 用于查询用户、部门、实验室、设备等信息，不会修改服务器状态 |
| POST | 创建 | 创建新资源 | 用于添加新用户、新设备、新借用记录等操作 |
| PUT | 更新 | 更新现有资源 | 用于修改已有用户信息、设备状态、借用记录等 |
| DELETE | 删除 | 删除资源 | 在项目中用于逻辑删除各类数据（通过设置deleted字段为1实现） |

## API文档访问方式

### 1. Swagger UI 交互式文档
- **访问地址**: [http://localhost:8080/swagger-ui/index.html](http://localhost:8080/swagger-ui/index.html)
- **功能**: 提供交互式界面，可以查看接口详情、测试API调用等

### 2. OpenAPI JSON格式文档
- **访问地址**: [http://localhost:8080/v3/api-docs](http://localhost:8080/v3/api-docs)
- **功能**: 提供标准的OpenAPI 3.0规范的JSON格式文档，可用于自动生成客户端代码或导入到其他API管理工具

## API模块详细说明

### 1. 测试接口

| 接口路径 | 方法 | 功能描述 | 响应数据 |
|---------|------|----------|----------|
| `/hello` | GET | 系统欢迎接口，返回系统运行状态信息 | 字符串: `"Hello, LabControl System is running!"` |
| `/health` | GET | 健康检查接口，用于监控系统状态 | 字符串: `"OK"` |

### 2. 用户管理 (`/api/user`)

#### 接口列表
| 接口路径 | 方法 | 功能描述 | 请求体 | 响应数据 |
|---------|------|----------|--------|----------|
| `/api/user` | GET | 获取所有用户列表 | 无 | `[{User对象数组}]` |
| `/api/user/{id}` | GET | 根据ID获取用户详情 | 无 | `{User对象}` |
| `/api/user` | POST | 添加新用户 | `{User对象}` | `{"result": true}` |
| `/api/user` | PUT | 更新用户信息 | `{User对象}` | `{"result": true}` |
| `/api/user/{id}` | DELETE | 删除用户（逻辑删除） | 无 | `{"result": true}` |

#### User对象结构
```json
{
  "id": 1,
  "username": "admin",
  "password": "123456",
  "name": "管理员",
  "departmentId": 1,
  "role": "ADMIN",
  "email": "admin@example.com",
  "phone": "13800138000",
  "status": "ACTIVE",
  "createdAt": "2024-01-01T00:00:00",
  "updatedAt": "2024-01-01T00:00:00",
  "deleted": 0
}
```

### 3. 部门管理 (`/api/department`)

#### 接口列表
| 接口路径 | 方法 | 功能描述 | 请求体 | 响应数据 |
|---------|------|----------|--------|----------|
| `/api/department` | GET | 获取所有部门列表 | 无 | `[{Department对象数组}]` |
| `/api/department/{id}` | GET | 根据ID获取部门详情 | 无 | `{Department对象}` |
| `/api/department` | POST | 添加新部门 | `{Department对象}` | `{"result": true}` |
| `/api/department` | PUT | 更新部门信息 | `{Department对象}` | `{"result": true}` |
| `/api/department/{id}` | DELETE | 删除部门（逻辑删除） | 无 | `{"result": true}` |

#### Department对象结构
```json
{
  "id": 1,
  "name": "计算机科学系",
  "description": "负责计算机相关教学和研究",
  "createdAt": "2024-01-01T00:00:00",
  "updatedAt": "2024-01-01T00:00:00",
  "deleted": 0
}
```

### 4. 实验室管理 (`/api/laboratory`)

#### 接口列表
| 接口路径 | 方法 | 功能描述 | 请求体 | 响应数据 |
|---------|------|----------|--------|----------|
| `/api/laboratory` | GET | 获取所有实验室列表 | 无 | `[{Laboratory对象数组}]` |
| `/api/laboratory/{id}` | GET | 根据ID获取实验室详情 | 无 | `{Laboratory对象}` |
| `/api/laboratory` | POST | 添加新实验室 | `{Laboratory对象}` | `{"result": true}` |
| `/api/laboratory` | PUT | 更新实验室信息 | `{Laboratory对象}` | `{"result": true}` |
| `/api/laboratory/{id}` | DELETE | 删除实验室（逻辑删除） | 无 | `{"result": true}` |

#### Laboratory对象结构
```json
{
  "id": 1,
  "name": "云计算实验室",
  "location": "科技楼301",
  "capacity": 40,
  "status": "AVAILABLE",
  "description": "配备高性能服务器的云计算实验环境",
  "createdAt": "2024-01-01T00:00:00",
  "updatedAt": "2024-01-01T00:00:00",
  "deleted": 0
}
```

### 5. 设备管理 (`/api/equipment`)

#### 接口列表
| 接口路径 | 方法 | 功能描述 | 请求体 | 响应数据 |
|---------|------|----------|--------|----------|
| `/api/equipment` | GET | 获取所有设备列表 | 无 | `[{Equipment对象数组}]` |
| `/api/equipment/{id}` | GET | 根据ID获取设备详情 | 无 | `{Equipment对象}` |
| `/api/equipment` | POST | 添加新设备 | `{Equipment对象}` | `{"result": true}` |
| `/api/equipment` | PUT | 更新设备信息 | `{Equipment对象}` | `{"result": true}` |
| `/api/equipment/{id}` | DELETE | 删除设备（逻辑删除） | 无 | `{"result": true}` |

#### Equipment对象结构
```json
{
  "id": 1,
  "name": "高性能服务器",
  "serialNumber": "SN123456",
  "model": "DELL R740",
  "manufacturer": "DELL",
  "laboratoryId": 1,
  "powerStatus": "ON",
  "networkStatus": "CONNECTED",
  "usageStatus": "AVAILABLE",
  "description": "用于云计算实验的服务器",
  "createdAt": "2024-01-01T00:00:00",
  "updatedAt": "2024-01-01T00:00:00",
  "deleted": 0
}
```

### 6. 设备借用管理 (`/api/equipment-borrow`)

#### 接口列表
| 接口路径 | 方法 | 功能描述 | 请求体 | 响应数据 |
|---------|------|----------|--------|----------|
| `/api/equipment-borrow` | GET | 获取所有借用记录 | 无 | `[{EquipmentBorrow对象数组}]` |
| `/api/equipment-borrow/{id}` | GET | 根据ID获取借用记录详情 | 无 | `{EquipmentBorrow对象}` |
| `/api/equipment-borrow` | POST | 新增借用申请 | `{EquipmentBorrow对象}` | `{"result": true}` |
| `/api/equipment-borrow` | PUT | 更新借用记录 | `{EquipmentBorrow对象}` | `{"result": true}` |
| `/api/equipment-borrow/{id}` | DELETE | 删除借用记录（逻辑删除） | 无 | `{"result": true}` |

#### EquipmentBorrow对象结构
```json
{
  "id": 1,
  "equipmentId": 1,
  "userId": 1,
  "borrowDate": "2024-01-10T09:00:00",
  "returnDate": null,
  "expectedReturnDate": "2024-01-15T17:00:00",
  "status": "BORROWED",
  "remarks": "用于项目开发",
  "createdAt": "2024-01-10T09:00:00",
  "updatedAt": "2024-01-10T09:00:00",
  "deleted": 0
}
```

### 7. 远程控制日志 (`/api/remote-control-log`)

#### 接口列表
| 接口路径 | 方法 | 功能描述 | 请求体 | 响应数据 |
|---------|------|----------|--------|----------|
| `/api/remote-control-log` | GET | 获取所有控制日志 | 无 | `[{RemoteControlLog对象数组}]` |
| `/api/remote-control-log/{id}` | GET | 根据ID获取日志详情 | 无 | `{RemoteControlLog对象}` |
| `/api/remote-control-log` | POST | 添加新日志 | `{RemoteControlLog对象}` | `{"result": true}` |
| `/api/remote-control-log/{id}` | DELETE | 删除日志（逻辑删除） | 无 | `{"result": true}` |

#### RemoteControlLog对象结构
```json
{
  "id": 1,
  "equipmentId": 1,
  "userId": 1,
  "operationType": "POWER_ON",
  "operationTime": "2024-01-10T10:30:00",
  "details": "远程开机操作",
  "result": "SUCCESS",
  "createdAt": "2024-01-10T10:30:00",
  "deleted": 0
}
```

## 通用数据说明

### 状态码说明
- `200 OK`: 请求成功
- `400 Bad Request`: 请求参数错误
- `404 Not Found`: 请求资源不存在
- `500 Internal Server Error`: 服务器内部错误

### 通用字段说明
- `id`: 自增主键ID
- `createdAt`: 创建时间（自动填充）
- `updatedAt`: 更新时间（自动填充）
- `deleted`: 逻辑删除标识（0:未删除, 1:已删除）

### 常用状态枚举值
- **设备状态(usageStatus)**: `AVAILABLE`(可用), `IN_USE`(使用中), `MAINTENANCE`(维护中), `UNAVAILABLE`(不可用)
- **电源状态(powerStatus)**: `ON`(开机), `OFF`(关机), `SLEEP`(休眠)
- **网络状态(networkStatus)**: `CONNECTED`(已连接), `DISCONNECTED`(未连接), `WEAK`(信号弱)
- **借用状态(status)**: `BORROWED`(已借出), `RETURNED`(已归还), `OVERDUE`(逾期), `APPLIED`(已申请)
- **用户状态(status)**: `ACTIVE`(活跃), `INACTIVE`(非活跃), `LOCKED`(锁定)

## 使用示例

### 前端调用示例（JavaScript）

```javascript
// 获取所有用户
fetch('http://localhost:8080/api/user')
  .then(response => response.json())
  .then(data => console.log(data))
  .catch(error => console.error('Error:', error));

// 添加新用户
const newUser = {
  username: 'testuser',
  password: '123456',
  name: '测试用户',
  departmentId: 1,
  role: 'USER',
  email: 'test@example.com',
  phone: '13900139000',
  status: 'ACTIVE'
};

fetch('http://localhost:8080/api/user', {
  method: 'POST',
  headers: {
    'Content-Type': 'application/json'
  },
  body: JSON.stringify(newUser)
})
.then(response => response.json())
.then(data => console.log('Success:', data))
.catch(error => console.error('Error:', error));
```

## 注意事项

1. 所有API接口均支持CORS跨域访问
2. API文档基于Swagger v3注解自动生成
3. 系统运行需要MySQL数据库支持（labcontrol数据库）
4. 所有删除操作均为逻辑删除，不会物理删除数据
5. 创建和更新操作时，时间戳字段会自动填充，无需手动设置
6. POST和PUT请求需要设置正确的Content-Type: application/json
7. 建议在生产环境中增加身份验证和权限控制机制