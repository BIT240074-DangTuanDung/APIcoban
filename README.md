# Bài tập API cơ bản

## Hướng dẫn kết nối API

### Thông tin cơ bản API
- **Base URL**: `https://localhost:7078`
- **Swagger UI**: `https://localhost:7078/swagger` (dùng để test trực tiếp các endpoint)

---

## Hướng dẫn test API bằng Postman

### 1. Chuẩn bị
- Đảm bảo server API đang chạy
- Mở Postman và tạo Collection mới (nếu cần)

### 2. Test từng endpoint

#### a. Lấy tất cả sản phẩm (GET)
1. Chọn phương thức **GET**
2. Nhập URL: `https://localhost:7078/api/products`
3. Nhấn **Send**
4. Kết quả: Danh sách các sản phẩm ban đầu

#### b. Lấy sản phẩm theo ID (GET)
1. Chọn phương thức **GET**
2. Nhập URL: `https://localhost:7078/api/products/1` (thay `1` bằng ID bạn muốn lấy)
3. Nhấn **Send**

#### c. Tạo sản phẩm mới (POST)
1. Chọn phương thức **POST**
2. Nhập URL: `https://localhost:7078/api/products`
3. Chọn tab **Body** → chọn **raw** → chọn định dạng **JSON**
4. Nhập dữ liệu JSON:
   ```json
   {
     "name": "Chuột không dây",
     "price": 500000
   }
   ```
5. Nhấn **Send**

#### d. Cập nhật sản phẩm (PUT)
1. Chọn phương thức **PUT**
2. Nhập URL: `https://localhost:7078/api/products/4` (thay `4` bằng ID sản phẩm bạn muốn cập nhật)
3. Chọn tab **Body** → chọn **raw** → chọn định dạng **JSON**
4. Nhập dữ liệu JSON (phải có cả `id`):
   ```json
   {
     "id": 4,
     "name": "Chuột không dây RGB",
     "price": 650000
   }
   ```
5. Nhấn **Send**

#### e. Xóa sản phẩm (DELETE)
1. Chọn phương thức **DELETE**
2. Nhập URL: `https://localhost:7078/api/products/4` (thay `4` bằng ID sản phẩm bạn muốn xóa)
3. Nhấn **Send**

---

### Các endpoint có sẵn

#### 1. Lấy tất cả sản phẩm
- **Phương thức**: `GET`
- **URL**: `/api/products`
- **Ví dụ (JavaScript)**:
  ```javascript
  fetch('https://localhost:7078/api/products')
    .then(response => response.json())
    .then(data => console.log(data))
    .catch(error => console.error('Lỗi:', error));
  ```

#### 2. Lấy sản phẩm theo ID
- **Phương thức**: `GET`
- **URL**: `/api/products/{id}`
- **Ví dụ (JavaScript)**:
  ```javascript
  const productId = 1;
  fetch(`https://localhost:7078/api/products/${productId}`)
    .then(response => {
      if (!response.ok) throw new Error('Không tìm thấy sản phẩm');
      return response.json();
    })
    .then(data => console.log(data))
    .catch(error => console.error('Lỗi:', error));
  ```

#### 3. Tạo sản phẩm mới
- **Phương thức**: `POST`
- **URL**: `/api/products`
- **Body**: JSON
- **Ví dụ (JavaScript)**:
  ```javascript
  const newProduct = {
    name: "Bàn phím cơ",
    price: 1200000
  };

  fetch('https://localhost:7078/api/products', {
    method: 'POST',
    headers: {
      'Content-Type': 'application/json'
    },
    body: JSON.stringify(newProduct)
  })
    .then(response => response.json())
    .then(data => console.log('Đã tạo:', data))
    .catch(error => console.error('Lỗi:', error));
  ```

#### 4. Cập nhật sản phẩm
- **Phương thức**: `PUT`
- **URL**: `/api/products/{id}`
- **Body**: JSON
- **Ví dụ (JavaScript)**:
  ```javascript
  const productId = 4;
  const updatedProduct = {
    id: productId,
    name: "Bàn phím cơ RGB",
    price: 1500000
  };

  fetch(`https://localhost:7078/api/products/${productId}`, {
    method: 'PUT',
    headers: {
      'Content-Type': 'application/json'
    },
    body: JSON.stringify(updatedProduct)
  })
    .then(response => {
      if (!response.ok) throw new Error('Cập nhật thất bại');
      console.log('Đã cập nhật thành công');
    })
    .catch(error => console.error('Lỗi:', error));
  ```

#### 5. Xóa sản phẩm
- **Phương thức**: `DELETE`
- **URL**: `/api/products/{id}`
- **Ví dụ (JavaScript)**:
  ```javascript
  const productId = 4;

  fetch(`https://localhost:7078/api/products/${productId}`, {
    method: 'DELETE'
  })
    .then(response => {
      if (!response.ok) throw new Error('Xóa thất bại');
      console.log('Đã xóa thành công');
    })
    .catch(error => console.error('Lỗi:', error));
  ```

### Lưu ý quan trọng
1. Đảm bảo server API đang chạy trước khi gọi API
2. Nếu dùng mobile app (React Native, Flutter,...) cần đảm bảo:
   - Thiết bị/máy ảo kết nối cùng mạng với máy chạy server
   - Hoặc dùng địa chỉ IP LAN của máy chạy server thay cho `localhost`
3. Với `https`, cần đảm bảo chứng chỉ SSL localhost được tin cậy trên thiết bị client

## Cấu trúc dữ liệu Product
```json
{
  "id": 1,
  "name": "Tên sản phẩm",
  "price": 1000000
}
```
