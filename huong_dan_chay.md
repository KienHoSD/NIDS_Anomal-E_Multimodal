Để chạy model ta cần tải các dependancy, các thư viện cần thiết nhưng phải tùy vào từng hệ điều hành, phiên bản Python, phiên bản PyTorch, CUDA hay CPU. Chủ yếu ta sẽ cần các thư viện như: DGL, PyTorch, NumPy, Pandas, Scikit-learn, Matplotlib, Seaborn, và một số thư viện khác để xử lý dữ liệu và trực quan hóa.
Vì vậy, để đơn giản, ta sẽ sử dụng Google Colab để chạy model này
Các bước thực hiện như sau:

1. Tải datasdet: NF-CSE-CIC-IDS2018-v2, NF-CSE-CIC-IDS2018-v3, NF-UNSW-NB15-v2, NF-UNSW-NB15-v3
Từ trang web: https://staff.itee.uq.edu.au/marius/NIDS_datasets/

2. Clean dataset: Chạy cleaning-nf...ipynb để chuyển các dataset thành định dạng .parquet (nhẹ hơn, load nhanh hơn vào RAM), không làm ảnh hưởng quá nhiều đến dữ liệu gốc.

3. Train mô hình:
Vì đã train trước và lưu lại parameter (các file tên best_dgi.pkl) nên không cần phải chạy bước này, nhưng có thể train lại model.
Vào từng phiên bản loại model notebook (unsw_v2, unsw_v3, cse_v2, cse_v3) -> chạy code đến một cell code lớn bị comment -> uncomment -> chạy node đó để train -> (tùy chọn) có thể tiếp tục chạy đến hết để classify, đánh giá model.
  Lưu ý:
    Sau khi train xong sẽ có được một file pickle (.pkl) mang tên bắt đầu với best_dgi... là các parameter của model sau khi train được lưu lại 
    Những lần chạy sau không cần phải train lại nên có thể comment cell code đó lại như truớc.
    Có thể uncomment các đoạn code ".to('cuda')" để train bằng GPU thay vì CPU (nếu có đủ VRAM nên train bằng GPU)
    Mỗi dataset đều được chích ra 10% (mỗi loại) để train, test -> giảm thời gian train, test (có đề cập trong bài báo)
    Tất cả các dataset đều KHÔNG CÓ căn chỉnh về 96% benign, 4% attack như trong bài báo, nhưng benign trong các bộ dataset đều chiếm phần lớn

4. Đánh giá model:
Mỗi lần chạy sau, chỉ cần chạy tất cả các cell sau khi đã train model để đánh giá.

5. Chạy phương pháp Multimodal:
Các notebook có tên ...fuse(multimodal).ipynb là dùng để chạy phương pháp Multimodal. Vì đã train model ở các bước trước nên không cần phải train lại (Multimodal không thay đổi cách train Model). Chạy tất cả các cell để đánh giá hiệu quả.

6. Chạy dataset từ bên ngoài sau khi train từ dataset tổng hợp (UNSW,CIC):
File mang tên ...test_external.ipynb là những notebook chạy cần dataset tổng hợp (để optimize các thuật toán Anomaly Dectection) và cần có dataset mới tự tạo bên ngoài để chạy (ví dụ mang tên clean_output.csv).
Cách chạy cũng tương tự, chạy tất cả các cell để đánh giá.
