# Hướng dẫn sử dụng Github

## Sử dụng Git

### Thao tác trên Local repository

Vấn đề: Bình thường ta sử dụng git là tạo repo trên server remote và add key rồi clone repo về và chỉnh sửa tại repo clone luôn. Nhưng bây giờ thì không, ta tạo một repo ở trên server remote và có được URL của repo.git. Ta sẽ tạo một thư mục làm việc trên local có kết nối đến repo đó trên server remote và push, pull từ thư mục local đấy.

Note: kiểu này thì mỗi lần push lên lại phải nhập tài khoản, mk. Nên dùng kiểu clone về và push lên cho đỡ nhâp mật khẩu

B1: vào thư mục local và gõ: git init

B2: tạo một file trong đó: vim xyz và thêm nội dung bất kỳ

b3: git add * 

B4: git commit -m 'addxyz'

B5: Liên kết với repo trên server remote: git remote add origin URL_repo_server <lên repo remote và lấy chỗ SSH và HTTPS>

P/S: origin là tên remote repository. Mặc định khi clone một repository thì nó tự đặt tên là origin.

B6: Kiểm tra liên kết với repo từ xa chưa: git remote -v

B7: Push dữ liệu lên server remote: git push origin master (vì liên kết với URL repo trên nên cần phải xác nhận user có được quyền vào repo đó không là nhập tài khoản và mật khẩu)

B8: Tạo file README trên github, khi có dữ liệu trên repository remote thì cần cập nhật lại repository local trước khi push từ data từ local lên server.

Nhưng cần chỉ định lấy từ brach nào: git pull <remote> <branch>. => git pull origin master.
  
Kiểm tra cấu hình git hiện tại: git config --list

### Thao tác trên remote repository: 
B1: Tạo repo trên server repository =>

B2: git clone URL_SSH => được repo trên local và thực hiện

B3: Tạo một file: vim abc và thêm nôi dung gì đó

B4: Xem trạng thái thực hiện: git status

Nó báo:

    Untracked files:
    (use "git add <file>..." to include in what will be committed)
    
        abc
        
nghĩa là: đã tìm thấy một sự thay đổi là file abc được thêm vào repo và chưa tracked (Untracked và abc màu đỏ) <chưa được đưa vào vùng staging>. Cần git add abc để tracked nó và nó sẽ được commit lên repository. Nếu muốn bỏ hãy xóa file đó: rm abc. Gõ git status lại:

    On branch master
    Your branch is up-to-date with 'origin/master'.
    nothing to commit, working directory clean


Nếu ta đã gõ: git add abc để thêm vào staging rồi <tên abc đã hiện màu xanh>, muốn bỏ file abc sang khỏi vùng stagging hãy gõ: git reset HEAD abc

    Màu đỏ: thay đổi của một file nào đó và chưa cho vào khu vực staging area
    Màu xanh: đã thêm vào staging area và sẵn sàng để commit. nó gọi là tracked: đánh dấu theo dõi trong staging area
    
git add/rm : thêm vào staging area để chuẩn bị commit
[git status: hiện màu xanh là đã vào vùng staging area: muốn bỏ unstag thì: git reset HEAD <tên file>]
[git status: màu đỏ nghĩa là git đã phát hiện sự thay đổi của một file nào đó: nếu là thêm thì hãy: git add <file> để vào tracked. Nếu là xóa thì có thể undo việc xóa bằng: git checkout -- <file>]
git commit -m "note_here"  : khi đã commit lại rồi, không thể quay lại được
[có thể dùng git commit -amend -m 'note_again_here']
git push, pull... :
Xem log: git log hoặc git log -p
