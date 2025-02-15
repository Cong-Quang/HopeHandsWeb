🚀TẠO NHÁNH MỚI (Branch) TRONG GITHUP

🔹 1.Lệnh kiểm tra danh sách hiện có:
(local):                    📌 git branch
(nhánh remote trên GITHUP): 📌 git branch -r
(full nhánh)              : 📌 git branch -a

🔹 2.Tạo nhánh mới và chuyển qua lại giữa các nhánh:
(tạo nhánh)     📌 git branch <namebranch>   
(chuyển nhánh)  📌 git checkout <namebranch>
(tạo và chuyển) 📌 git checkout -b <namebranch>

🔹 3.Đẩy nhánh mới lên GitHub:
(push khi có thay đổi trong nhánh)
        📌 git status
        📌 git add .
        📌 git commit -m 'add_text_here'
        📌 git push origin <namebranch>

🔹 4. Xoá nhánh:
(local):       📌 git branch -d <namebranch>
(trên GITHUP): 📌 git push origin --delete <namebranch>


    




