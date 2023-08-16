# GenEmailByInfoFPT

```js
// Lấy đối tượng bảng dựa trên ID
var table = document.getElementById("id");

function convertVietnameseToEnglish(text) {
    const vietnameseChars = "ÁÀẢẠÃÂẤẦẨẬẪĂẮẰẲẶẴĐÉÈẺẸẼÊẾỀỂỆỄÍÌỈỊĨÓÒỎỌÕÔỐỒỔỘỖƠỚỜỞỢỠÚÙỦỤŨƯỨỪỬỰỮÝỲỶỴỸ";
    const englishChars = "AAAAAAAAAAAAAAAAADEEEEEEEEEEEEIIIIIOOOOOOOOOOOOOOOOUUUUUUUUUUUUYYYYY";
    
    let convertedText = "";
    
    for (let i = 0; i < text.length; i++) {
        const char = text.charAt(i);
        const index = vietnameseChars.indexOf(char);
        if (index !== -1) {
            convertedText += englishChars.charAt(index);
        } else {
            convertedText += char;
        }
    }
    
    return convertedText;
}

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
    var surname = row.querySelector("td:nth-child(5)").textContent.trim().normalize("NFD").replace(/[\u0300-\u036f]/g, "");

    if(surname != NaN && surname != null){
        var arrSurname = surname.split(" ");
        var lenArr = arrSurname.length;
        var abbreviatedSurname = "";

        for (var j = 0; j < lenArr; j++) {
            abbreviatedSurname += arrSurname[j].charAt(0);
            
        }
        // console.log(abbreviatedSurname);
        surname = abbreviatedSurname;
    }

    var middleSurname = row.getElementsByTagName("td")[5].textContent.trim().normalize("NFD").replace(/[\u0300-\u036f]/g, "");

    // Tạo địa chỉ email theo định dạng
    var email = convertVietnameseToEnglish(middleSurname) + convertVietnameseToEnglish(code.charAt(0)) + convertVietnameseToEnglish(surname) + member + "@fpt.edu.vn";
    if (i == 0) {
        arrEmail += email;
    } else {
        arrEmail += "," + email;
    }

}
// In ra địa chỉ email tạo được
console.log(arrEmail);
```
