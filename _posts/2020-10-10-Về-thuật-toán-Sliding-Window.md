---
layout: post
title: Về thuật toán Sliding Window
date: 2020-10-10
tags: Algorithms Programming
---

<!--- content here --->
Trong quá trình chuẩn bị, mình đã đọc qua rất nhiều bài viết ấn tượng trên các diễn đàn khác nhau, trong đó có một bài viết của tác giả Jordan Moore đã mượn một câu hỏi trong quyển Hoàng tử Bé để mô tả về tính hoàn hảo của một thuật toán. Mình xin được trích dẫn ở dưới đây:

"Perfection is achieved, not when there is nothing more to add, but when there is nothing left to take away." (tạm dịch: Chúng ta đạt được hoàn hảo, không phải khi không còn gì có thể thêm vào, mà không còn gì có thể lấy đi nữa.)

Thuật toán được định nghĩa là một lời diễn giải của các bước để hoàn thành một mục tiêu gì đấy. Thuật toán có ở khắp mọi nơi theo định nghĩa này, khi bạn đánh răng buổi sáng, khi bạn ra ngoài, vân vân và mây mây. 

Đối với lập trình viên, thuật toán hoàn hảo nhất là khi dùng số bước ít nhất, tốn ít thời gian nhất và ít bộ nhớ nhất có thể. Vậy nên có thể nói, theo tư tưởng của Antoine de Saint-Exupéry, việc của một lập trình viên không phải là thêm mắm thêm muối vào thuật toán của mình, mà lấy đi những bước không cần thiết. Khi không còn gì có thể lấy ra, lập trình viên mới có được một thuật toán hoàn hảo.

Có nhiều cách để đạt được độ chín muồi trong việc viết thuật toán, Sliding Window là một trong số đó. Mình mong các bạn sẽ hiểu rõ hơn về thuật toán này sau bài viết hôm nay.

## Định nghĩa

Sliding Window là thuật toán được sử dụng nhiều trong các bài toán liên quan tới String và Array. Cũng giống như tên gọi, thuật toán sẽ tạo ra một window để lưu một phần của dữ liệu, và window này sẽ trượt qua trượt lại để lưu những phần khác nhau của dữ liệu đó.

## Cách hoạt động
Để minh hoạ cho cách hoạt động của thuật toán Sliding Window, mình sẽ dùng ví dụ sau: "Cho một array số tự nhiên dương, tìm cặp số tự nhiên kề nhau sao cho tổng của cặp số này là lớn nhất."

Giả sử input của bài toán là [1, 5, 7, 9, 0, 2]

Trong bài toán này, window sẽ bao gồm một cặp số, bắt đầu từ cặp số đầu tiên. Đối với mỗi cặp số được lưu trong window, mình sẽ tính tổng và cập nhật kết quả nếu cửa sổ này cho ra tổng lớn hơn tất cả những cửa sổ trước đó.

Vậy, pseudocode của bài toán này là:
	khởi tạo 2 pointers, pointer1 = 0 và pointer2 = 1
	trượt window cho tới khi duyệt hết array
		tính tổng mỗi window.
		cập nhật tổng lớn nhất


## Một số loại Window
Mong rằng đến đây thì bạn đã hiểu được "sơ sơ" cách hoạt động của thuật toán Sliding Window. Phần này sẽ tập trung vào hai loại window mà bạn có thể sử dụng, tuỳ vào yêu cầu của bài toán.

### Fixed-size Window
Kích thước của Window trong những bài toán này sẽ được giữ nguyên. Ví dụ như bài toán có thể cho một array gồm các số tự nhiên và yêu cầu tìm 3 số liền kề nhau có tổng lớn nhất. Thông thường, chúng ta sẽ cần một số biến khác để lưu trạng thái của Window, tuỳ yêu cầu bài toán mà biến này có thể là Integer hay một số loại phức tạp hơn như List, Queue hay Deque.

### Two-pointer Window
Kích thước của Window trong những bài toán dạng này sẽ thay đổi tuỳ theo yêu cầu của bài toán. Một số kiểu Window trong dạng này có thể kể đến như Fast/Slow và Fast/Catchup dưới đây.

### Fast/Slow
Trong loại này, bạn sẽ cần có một pointer chạy cực nhanh và một pointer chạy cực chậm. Fast pointer sẽ giúp tăng kích thước của Window, trong khi đó, Slow pointer sẽ giúp giảm kích thước của Window.

Ví dụ như trong bài toán sau: "Cho string S và string T. Tìm substring có độ dài nhỏ nhất của S chứa tất cả các chữ cái của T." Fast pointer sẽ tăng kích thước của Window cho tới khi Window chứa tất cả các chữ cái của T. Khi đã tìm được Window phù hợp, Slow pointer sẽ thu nhỏ kích thước của Window cho tới khi Window không còn phù hợp với yêu cầu bài toán nữa.

### Fast/Catchup
Cũng giống như Fast/Slow Window, bạn cũng sẽ cần một Fast pointer chạy cực nhanh và một Slow pointer chạy cực chậm. Tuy nhiên, lần này chúng ta sẽ bổ sung một siêu năng lực cho Slow pointer, đó là teleport và đổi tên pointer này thành Catchup pointer.

Ví dụ như trong bài toán sau: "Cho array gồm các số tự nhiên, tìm dãy các số tự nhiên liên tiếp sao cho tổng của chúng lớn nhất." Trong mảng này, dĩ nhiên sẽ có các số âm và dương. Fast pointer lúc này sẽ làm nhiệm vụ thu thập các số tự nhiên để tăng tổng của dãy hiện tại. Tuy nhiên, khi Fast pointer đột nhiên "cộng nhầm" và biến tổng của dãy hiện tại thành số âm, Catchup pointer sẽ "teleport" đến vị trí của Fast pointer để giúp Fast pointer bắt đầu lại từ đầu.

Vậy là xong! Hy vọng rằng qua bài viết này, mình đã cung cấp "đủ" thông tin về thuật toán Sliding Window để giúp bạn chinh phục được những bài toán khó nhằn trong tương lai. Xin cảm ơn, và hẹn gặp lại trong những bài viết tiếp theo!



