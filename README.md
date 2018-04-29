# Hướng dẫn sử dụng Github

## Sử dụng Git

### Thao tác trên Local repository

Mô hình trên local:

* Staging Area là một khu vực trung gian, là khu vực sẽ lưu trữ những thay đổi của bạn trên tập tin để nó có thể được commit, vì muốn commit tập tin nào thì tập tin đó phải nằm trong Staging Area.

* Commit là một hành động để Git lưu lại một bản chụp (snapshot) của các sự thay đổi trong thư mục làm việc, và các tập tin và thư mục được thay đổi đã phải nằm trong Staging Area

* Commit xong vào khu vực repository trên local, muốn đấy lên repository trên server dùng:git push

Hình minh họa:

![](/image/1.jpg)

Vấn đề: Bình thường ta sử dụng git là tạo repo trên server remote và add key rồi clone repo về và chỉnh sửa tại repo clone luôn. Nhưng bây giờ thì không, ta tạo một repo ở trên server remote và có được URL của repo.git. Ta sẽ tạo một thư mục làm việc trên local có kết nối đến repo đó trên server remote và push, pull từ thư mục local đấy.

Note: kiểu này thì mỗi lần push lên lại phải nhập tài khoản, mk. Nên dùng kiểu clone về và push lên cho đỡ nhâp mật khẩu

* B1: vào thư mục local và gõ: git init

* B2: tạo một file trong đó: vim xyz và thêm nội dung bất kỳ

* B3: git add * 

* B4: git commit -m 'addxyz'

* B5: Liên kết với repo trên server remote: git remote add origin URL_repo_server <lên repo remote và lấy chỗ SSH và HTTPS>

P/S: origin là tên remote repository. Mặc định khi clone một repository thì nó tự đặt tên là origin.

* B6: Kiểm tra liên kết với repo từ xa chưa: git remote -v

* B7: Push dữ liệu lên server remote: git push origin master (vì liên kết với URL repo trên nên cần phải xác nhận user có được quyền vào repo đó không là nhập tài khoản và mật khẩu)

* B8: Tạo file README trên github, khi có dữ liệu trên repository remote thì cần cập nhật lại repository local trước khi push từ data từ local lên server.

Nhưng cần chỉ định lấy từ brach nào: git pull <remote> <branch>. => git pull origin master.
  
Kiểm tra cấu hình git hiện tại: git config --list

### Thao tác trên remote repository: 

* B1: Tạo repo trên server repository =>

* B2: git clone URL_SSH => được repo trên local và thực hiện

* B3: Tạo một file: vim abc và thêm nôi dung gì đó

* B4: Xem trạng thái thực hiện: git status

* Nó báo:

      Untracked files:
      (use "git add <file>..." to include in what will be committed)
    
        abc
        
* Nghĩa là: đã tìm thấy một sự thay đổi là file abc được thêm vào repo và chưa tracked (Untracked và abc màu đỏ) <chưa được đưa vào vùng staging>. Cần git add abc để tracked nó và nó sẽ được commit lên repository. Nếu muốn bỏ hãy xóa file đó: rm abc. Gõ git status lại:

      On branch master
      Your branch is up-to-date with 'origin/master'.
      nothing to commit, working directory clean


* Nếu ta đã gõ: git add abc để thêm vào staging rồi <tên abc đã hiện màu xanh>, muốn bỏ file abc sang khỏi vùng stagging hãy gõ: git reset HEAD abc

      Màu đỏ: thay đổi của một file nào đó và chưa cho vào khu vực staging area
      Màu xanh: đã thêm vào staging area và sẵn sàng để commit. nó gọi là tracked: đánh dấu theo dõi trong staging area
    
* Sau đó ta gõ để commit abc vào repository: git commit -m 'create_abc'. Gõ git status:

      1 file changed, 2 insertions(+)
      create mode 100644 abc

      On branch master
      Your branch is ahead of 'origin/master' by 1 commit.
        (use "git push" to publish your local commits)
      nothing to commit, working directory clean
      
 * Nếu đột nhiên thấy phần comment của git commit bị sai, muốn sửa lại comment không người khác hiểu lầm thì gõ: git commit -amend -m 'note_again_here'
      
* Một commit đang đợi để push, muốn hủy commit không push hãy gõ: git reset --soft HEAD^ . Gõ git status lại: nó sẽ về trạng thái để commit
 
      On branch master
      Your branch is up-to-date with 'origin/master'.
      Changes to be committed:
        (use "git reset HEAD <file>..." to unstage)

        new file:   abc


Bước 5: Nếu là xóa một file: rm abc thì có thể undo việc xóa bằng: git checkout -- <file>. Vì vậy nên xóa bằng git rm abc => commit => push.

B6: Xem log: git log --graph --oneline --all

### Thao tác nâng cao

Branch: Nhánh so với cái chính: khi muốn tạo một tính năng mới cho code hay thử nghiệm gì đó mới mà không muốn đụng vào cái chính thường là master thì hãy tạo branch làm độc lập, khi OK rồi hãy gộp về master 

* Tạo branch mới ví dụ dev: git branch dev < branch dev có hết luôn code của master>

* Xem đang ở brach nào: git branch

* Sau khi tạo một file và git add, commit đầy đủ: để push branch dev lên hãy: git push origin dev

* Clone branch : git clone -b dev git@github.com:kudokunn/Github.git 

<Hoặc sử dụng git checkout dev để chuyển sang branch dev và thao tác trong đó, cần thì lại về master>

* Chuyển sang branch khác ví dụ sang master: git checkout master

* Để merger gộp branch dev đã tạo trước về master làm:
  
        git checkout master
        git pull
        git checkout test
        git pull
        git rebase -i master
        git checkout master
        git merge test

Note: không được dùng rebase trên public branch, như master branch.

    git checkout master
    git rebase -i test
    
* Sau khi gộp branch xong có thể xóa branch dev: git branch -D dev

### Mốt số lệnh khác:

* Git Pull: câu lệnh git pull thực ra là viết tắt của git pull origin master. Trong đó:

    origin là tên của kho chứa từ xa (hay remote repository).
    master là tên của nhánh trên kho chứa từ xa. Một kho chứa có thể có nhiều nhánh khác nhau.
    
* Để liệt kê các kho chứa từ xa bạn có thể dùng câu lệnh sau:

      $ git remote -v

* Để liệt kê cách nhánh của các kho chứa:

      $ git branch -a

* Về bản chất khi chạy câu lệnh git pull origin master thực sự là bạn đang sử dụng hai câu lệnh phía sau:

      $ git fetch origin master

và:

      $ git merge origin master

Câu lệnh git fetch origin master sẽ truy vấn thông tin của kho chứa từ xa trên máy chủ remote và sau đó kéo về máy local những thay đổi này. Tiếp đó câu lệnh trên sẽ thực hiện việc so sánh những thay đổi mới kéo về máy local và hiển thị thông tin.

Câu lệnh git merge orign master sẽ gộp những thay đổi mới kéo về (dùng câu lệnh git fetch ở trên) từ máy chủ từ xa với nhánh hiện tại trên máy local.

=> Vấn đề: Nếu từ branch nào đó là dev chằng hạn mà gõ: git pull origin master thì nó sẽ fetch và merger data từ master về dev.
            Nếu từ branch master gõ git pull từ dev: git pull origin dev thì vẫn pull được data từ dev về master 

* Git pull request:

Thông thường khi làm với Git mỗi lập trình viên sẽ tạo một branch mới khác với master để phát triển một tính năng mới. Giả sử nhánh mà lập trình viên tạo ra để phát triển tính năng có tên là my_feature. Trong trường hợp này sau khi đẩy commit trên nhánh này trên nhánh tương ứng my_feature ở kho chứa từ xa origin thì để các lập trình viên khác có thể kéo về được commit này thì quản trị viên trên máy chủ từ xa cần thực hiện việc gộp commit ở nhánh my_feature về nhánh master.

Pull request là một yêu cầu gửi tới quản trị viên kho chứa từ xa gộp commit mới được tạo ra từ nhanh my_feature về nhánh master để các lập trình viên khác có thể pull về được.

### Vấn đề conflic: 

Khi bạn làm việc với nhiều branch, nhảy qua nhảy về, commit, sửa chung một dòng code, cũng sẽ xảy ra conflict. Bản chất conflic là khi merge code lại mà dòng đó có nhiều người chỉnh sửa nên git không biết lấy dòng nào và báo conflic để hỏi người dùng xem lấy dòng nào hay giữ cả hai dòng code (fix đấy)

### Ví dụ: Tạo repo local

    $ mkdir demo_conflict
    $ cd demo_conflict
    $ git init
    Initialized empty Git repository in /Users/user/Desktop/demo_conflict/.git/
    
#### Tạo nhánh master:

    $ git checkout -b master # tạo branch master
    Switched to a new branch 'master'
    $ touch file_in_master # tạo file
    $ echo "line 1 in master" >> file_in_master # thêm dòng 1 file 
    $ git add file_in_master  # thêm vào staging area
    $ git commit -m "init and add first line in master" # lưu thay đổi vào repository
    
 #### Tạo nhánh conflic
 
    $ git checkout -b conflict # tạo nhánh branch conflic
    Switched to a new branch 'conflict'
    $ git commit -m "Add line 2 in conflict branch" >> file_in_master # thêm dòng 2 vào file
    $ git add file_in_master # thêm vào staging
    $ git commit -m "Add line 2 in conflict branch" # lưu vào repository
    $ cat file_in_master
    line 1 in master
    Add line 2 in conflict branch
    
 #### Tạo conflic khi merge:
 
    $ git checkout master
    Switched to branch 'master'
    $ echo "line 2 in master branch, this will lead to conflict issue" >> file_in_master 
    $ git add file_in_master 
    $ git commit -m "add line 2 in master branch, this will lead to conflict issue"
    $ git merge conflic # gộp từ branch conflic into master
    [master b5fb839] add line 2 in master branch, this will lead to conflict issue
     1 file changed, 1 insertion(+)
    $ git merge conflict
    CONFLICT (content): Merge conflict in file_in_master
    Recorded preimage for 'file_in_master'
    Automatic merge failed; fix conflicts and then commit the result.
    
#### Fix conflic: chỉ cần sửa là lấy một trong hai đoạn code hay giữ cả hai và xóa mấy dòng <<<<<<<HEAD >>>>>>>>> conflic
    
    $ vim file_in_master
    
    line 1 in master
    <<<<<<< HEAD
    line 2 in master branch, this will lead to conflict issue
    =======
    line 2 in conflict branch
    >>>>>>> conflict
    
Xong git add, git commit file đó bình thường
    
