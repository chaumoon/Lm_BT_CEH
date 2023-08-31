link bài tập: https://overthewire.org/wargames/bandit/<br>
0. bandit0
- dùng ssh truy cập và bandit0 trên cổng 2220: ssh bandit0@bandit.labs.overthewire.org -p 2220
- nhập mật khẩu: bandit0

1. bandit1
- dùng lệnh 'll' để liệt kê ra danh sách file<br>

![image](https://github.com/chaumoon/CEH/assets/127403046/d1682eae-d2ca-45c0-bae0-445af1b7b0ee)<br>

- dùng lệnh 'cat' đọc file 'readme' thu được mật khẩu: NH2SXQwcBdpmTEzi3bvBHMM9H66vVXjL<br>

2. bandit2
- truy cập vào bandit1 bằng ssh và mật khẩu vừa thu được
- dùng ll để liệt kê danh sách -> thu được file '-'
- vì file là kí tự đặc biệt -> dùng lệnh 'cat ./-' để đọc file
- thu được mật khẩu: rRGizSaX8Mk1RTb1CNQoXTcYZWU6lgzi<br>

3. bandit3
- dùng lệnh 'll' thu được file 'spaces in this filename'
- đây cx là file đặc biệt vì tên file có khoảng trống -> xài lệnh 'cat "spaces in this filename"'
- thu được mật khẩu: aBZ0W5EmUfAf7kHTQeOwd8bauFJ2lAiG<br>

4. bandit4
- dùng lệnh 'll' ta thu được <br>

![image](https://github.com/chaumoon/CEH/assets/127403046/6f6d734e-4b2f-4547-90bf-1d8a2134de05)<br>

- xuất hiện thư mục 'inhere/' -> truy cập và thư mục bằng lệnh 'cd inhere/'
- dùng lệnh 'll' ta thu được<br>

![image](https://github.com/chaumoon/CEH/assets/127403046/2399984b-897c-40bd-ac96-e572d6f59581)<br>

- ta thu được mật khẩu khi đọc file '.hidden': 2EW7BBsr6aMMoJ2HjW067dm8EgX26xNe<br>

5. bandit5
- truy cập và thư mục 'inhere/' và dùng lệnh 'll' thu được <br>

![image](https://github.com/chaumoon/CEH/assets/127403046/2d10db5b-51da-4764-a5ac-207d86eab035)<br>

- dùng lệnh 'file ./-file0*' để xem loại file:<br>

![image](https://github.com/chaumoon/CEH/assets/127403046/8e157188-f79e-4915-bf9f-e8951e1b3803)<br>

-> -file07 là file đọc được, đọc file -> mật khẩu: lrIWWI6bB37kxfiCQZqUdOIYfr6eEeqR

6. bandit6
- truy cập vào thư mục 'inhere/' dùng lệnh find: find . -readable -size 1033c ! -executable<br>

![image](https://github.com/chaumoon/CEH/assets/127403046/80d2e695-5ae1-4f88-a997-441a64494fc9)<br>

- đọc file -> thu được mật khẩu: P4L4vucdmLnm8I7Vl7jG1ApGSfjYKqJU

7. bandit7
- dùng lệnh find để tìm file thỏa mãn điều kiện: find / -user bandit7 -group bandit6 -size 33c 2>/dev/null
- thu được file: /var/lib/dpkg/info/bandit7.password
- đọc file ta thu được mật khẩu: z7WtoNQU2XfjmMtWA8u5rN4vzqu4v99S<br>

8. bandit8
- đọc file dât.txt dùng lệnh 'grep' để tìm từ 'millionth': cat data.txt | grep millionth
- ta thu được: millionth       TESKZC0XvTetK0S9xNwm25STk5iWrBvP<br>

9. bandit9
- tệp data.txt có mật khẩu là dòng chỉ xuất hiện 1 lần
- sắp xếp tệp bằng lệnh 'sort', sau đó dùng 'uniq -u' để tìm dòng xuất hiện 1 lần: sort data.txt | uniq -u
- thu được mật khẩu: EN632PlfYiZbn3PhVK3XOGSlNInNE00t<br>

10. bandit10
- tệp chỉ đọc được bằng 'strings' và bắt đầu bằng kí tự '=': strings data.txt | grep "="
- ta thu được: <br>

![image](https://github.com/chaumoon/CEH/assets/127403046/aed2c734-9258-4b28-a8e1-b8751a6480a6)<br>

- mật khẩu: G7w8LIi6J3kTb8A7j9LgrywtEUlyyp6s
