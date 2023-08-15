# GenEmailByInfoFPT

```html
// Lấy đối tượng bảng dựa trên ID
var table = document.getElementById("id");

// Lấy danh sách các hàng trong tbody
var rows = table.getElementsByTagName("tbody")[0].getElementsByTagName("tr");
console.log(rows.length);
var arrEmail = ""
// Duyệt qua từng hàng và tạo địa chỉ email
var len = rows.length
for (var i = 0; i < len; i++) {
    var row = rows[i];
    
    // Lấy các thông tin từ các ô tương ứng
    var member = row.getElementsByTagName("td")[2].textContent.trim();
    var code = row.getElementsByTagName("td")[3].textContent.trim().normalize("NFD").replace(/[\u0300-\u036f]/g, "");
    
    // Xử lý tên họ
    var surname = row.getElementsByTagName("td")[4].textContent.trim().normalize("NFD").replace(/[\u0300-\u036f]/g, "");
    var middleSurname = row.getElementsByTagName("td")[5].textContent.trim().normalize("NFD").replace(/[\u0300-\u036f]/g, "");
    
    // Tạo địa chỉ email theo định dạng
    var email = middleSurname + code.charAt(0)+ surname.charAt(0)+member + "@fpt.edu.vn";
    if(i==0){
        arrEmail += email;
    } else{
        arrEmail +=","+ email;
    }
      
}
// In ra địa chỉ email tạo được
console.log(arrEmail);
```
