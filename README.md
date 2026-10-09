BÁO CÁO THỰC HÀNH KIỂM THỬ API BẰNG POSTMAN
1. Mục tiêu thực hành
Tìm hiểu công cụ kiểm thử API Postman.
Làm quen với các phương thức HTTP: GET, POST, PUT và DELETE.
Thực hành gửi request và kiểm tra response từ máy chủ.
Viết test script bằng JavaScript để tự động kiểm tra kết quả.
Tổ chức các request thành Collection và xuất dữ liệu kiểm thử.
Sử dụng GitHub để lưu trữ sản phẩm và báo cáo thực hành.
2. Công cụ và môi trường
Công cụ	Mục đích
Postman Web	Gửi request và kiểm thử API
JSONPlaceholder	API mẫu dùng để thực hành
GitHub	Lưu trữ Collection, ảnh và báo cáo
Markdown	Trình bày báo cáo trong README.md

API sử dụng: https://jsonplaceholder.typicode.com/

JSONPlaceholder là dịch vụ API giả lập, phù hợp để thực hành các thao tác CRUD mà không cần xây dựng máy chủ riêng.

3. Nội dung thực hành
3.1. Kiểm thử GET – Lấy danh sách bài viết
Method: GET
URL: https://jsonplaceholder.typicode.com/posts
Mục đích: Lấy danh sách bài viết từ API.

Kết quả mong đợi:<img width="2282" height="1312" alt="image" src="https://github.com/user-attachments/assets/3415d384-25a3-4ce4-8072-3b0c4fdc17d9" />


HTTP status code: 200 OK.
Response có định dạng JSON.
Dữ liệu trả về là một danh sách bài viết.

Ảnh minh họa:<img width="2088" height="1238" alt="image" src="https://github.com/user-attachments/assets/5c0bbe97-2863-4b74-8e02-e3e91aaea40b" />





3.2. Kiểm thử GET – Lấy thông tin một bài viết
Method: GET
URL: https://jsonplaceholder.typicode.com/posts/1
Mục đích: Lấy thông tin bài viết có ID bằng 1.

Kết quả mong đợi:<img width="2088" height="1238" alt="image" src="https://github.com/user-attachments/assets/99447dfb-e68b-4b77-ac09-0686aa2c8a7b" />


HTTP status code: 200 OK.
Response chứa các trường userId, id, title và body.
Giá trị id bằng 1.

Test script:

pm.test("Status code is 200", function () {
    pm.response.to.have.status(200);
});

pm.test("Response is valid JSON", function () {
    pm.response.to.be.json;
});

pm.test("Post ID equals 1", function () {
    const data = pm.response.json();
    pm.expect(data.id).to.eql(1);
});

pm.test("Title is not empty", function () {
    const data = pm.response.json();
    pm.expect(data.title).to.be.a("string");
    pm.expect(data.title.length).to.be.greaterThan(0);
});

Kết quả kiểm thử: <img width="2356" height="688" alt="image" src="https://github.com/user-attachments/assets/0184f02f-f158-4f60-8e30-e2214e8f9be4" />

3.3. Kiểm thử POST – Tạo bài viết
Method: POST
URL: https://jsonplaceholder.typicode.com/posts
Mục đích: Gửi dữ liệu JSON để mô phỏng tạo bài viết mới.

Request Body:

{
  "userId": 1,
  "title": "Postman Testing",
  "body": "This is a test post created using Postman."
}

Kết quả mong đợi:

HTTP status code: 201 Created.
Response chứa thông tin bài viết được gửi.
Tiêu đề trả về là Postman Testing.

Test script:

pm.test("Status code is 201", function () {
    pm.response.to.have.status(201);
});

pm.test("Title matches submitted data", function () {
    const data = pm.response.json();
    pm.expect(data.title).to.eql("Postman Testing");
});

pm.test("Response contains an ID", function () {
    const data = pm.response.json();
    pm.expect(data).to.have.property("id");
});
Ảnh minh họa:
<img width="2316" height="1314" alt="image" src="https://github.com/user-attachments/assets/dea9cd15-4f62-4d6d-ae29-228b9b191b61" />

3.4. Kiểm thử PUT – Cập nhật bài viết
Method: PUT
URL: https://jsonplaceholder.typicode.com/posts/1
Mục đích: Gửi dữ liệu cập nhật cho bài viết có ID bằng 1.

Request Body:

{
  "userId": 1,
  "id": 1,
  "title": "Updated by Postman",
  "body": "Updated content for API testing."
}

Kết quả mong đợi:

HTTP status code: 200 OK.
Response có tiêu đề Updated by Postman.

Test script:

pm.test("Status code is 200", function () {
    pm.response.to.have.status(200);
});

pm.test("Title was updated", function () {
    const data = pm.response.json();
    pm.expect(data.title).to.eql("Updated by Postman");
});

Kết quả kiểm thử: 
<img width="2266" height="1288" alt="image" src="https://github.com/user-attachments/assets/6ed51ebd-dbba-4687-94c6-30da3048cc34" />

3.5. Kiểm thử DELETE – Xóa bài viết
Method: DELETE
URL: https://jsonplaceholder.typicode.com/posts/1
Mục đích: Thực hiện request xóa bài viết có ID bằng 1.

Kết quả mong đợi:

HTTP status code: 200 OK theo phản hồi thông thường của JSONPlaceholder.
Response được kiểm tra theo kết quả API trả về.

Test script:

pm.test("Status code is 200", function () {
    pm.response.to.have.status(200);
});

Kết quả kiểm thử: [Điền kết quả thực tế]

Ảnh minh họa:
<img width="2248" height="1292" alt="image" src="https://github.com/user-attachments/assets/5898b756-4a47-45d5-96c7-56337138128f" />




Lưu ý: JSONPlaceholder mô phỏng thao tác tạo, cập nhật và xóa. Các thay đổi không được lưu vĩnh viễn trên máy chủ.

4. Kết quả kiểm thử tổng hợp
STT	Trường hợp kiểm thử	Phương thức	Kết quả thực tế
1	Lấy danh sách bài viết	GET	[Điền kết quả]
2	Lấy bài viết ID 1	GET	[Điền kết quả]
3	Tạo bài viết	POST	[Điền kết quả]
4	Cập nhật bài viết	PUT	[Điền kết quả]
5	Xóa bài viết	DELETE	[Điền kết quả]
Tổng kết số liệu
Tổng số request: [Điền số lượng]
Tổng số test đã chạy: [Điền số lượng]
Số test thành công: [Điền số lượng]
Số test thất bại: [Điền số lượng]
Kết quả chạy Collection




5. Cấu trúc repository
postman-api-testing/
├── README.md
├── collections/
│   └── postman-api-testing.postman_collection.json
└── screenshots/
    ├── 01-get-posts.png
    ├── 02-get-single-post.png
    ├── 03-post-request.png
    ├── 04-test-results.png
    ├── 05-collection-runner.png
    ├── 06-put-request.png
    └── 07-delete-request.png
6. Kết luận

Qua bài thực hành, sinh viên đã tìm hiểu cách sử dụng Postman để gửi các HTTP request, kiểm tra dữ liệu phản hồi và xây dựng test script tự động bằng JavaScript.

Các phương thức GET, POST, PUT và DELETE giúp làm quen với những thao tác cơ bản của API. Việc sử dụng Collection hỗ trợ tổ chức các trường hợp kiểm thử, trong khi GitHub giúp lưu trữ sản phẩm và trình bày kết quả thực hành.

7. Tài liệu tham khảo
Video hướng dẫn do giảng viên cung cấp: https://www.youtube.com/watch?v=MFxk5BZulVU
Postman Learning Hub: https://www.postman.com/learn/
Postman Test Scripts: https://learning.postman.com/docs/tests-and-scripts/write-scripts/test-scripts/
JSONPlaceholder: https://jsonplaceholder.typicode.com/
