## Certificate Template Exploitation

### Enumeration
Xác định các certificate template có dấu hiệu cấu hình yếu hoặc được công cụ phân loại là dễ bị lạm dụng. Các template kiểu này thường được rà soát trước để tìm trường hợp cho phép enrollment quá rộng hoặc hỗ trợ impersonation thông qua thuộc tính subject/SAN.  

```text
Certify.exe enum-templates --filter-vulnerable
```

### Certificate Request
Trong các trường hợp cấu hình sai kiểu ESC1, template có thể cho phép requester chỉ định danh tính mục tiêu trong certificate request. Điều này khiến certificate được cấp có thể đại diện cho một principal khác nếu template vừa cho phép enroll vừa cho phép requester cung cấp subject hoặc UPN.

```text
Certify.exe request --ca <CA-Name> --template <Template-Name> --upn <Target-UPN>
```

### Kerberos Authentication via Certificate
Sau khi có certificate hợp lệ, có thể dùng certificate đó trong luồng PKINIT để yêu cầu Kerberos TGT. Một số công cụ cũng hỗ trợ lấy thêm thông tin credential liên quan từ quá trình xác thực bằng certificate.

```text
Rubeus.exe asktgt /user:<Target-User> /certificate:<Base64-or-PFX> /getcredentials
```
