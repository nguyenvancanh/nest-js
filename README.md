# nest-js

Nếu bạn đã từng làm việc với một dự án NodeJs hay đã từng xây dựng một REST API cho một ứng dụng thì bạn sẽ nhận ra sự tẻ nhạt cùng như buồn chán trong quá trinh duy trì ứng dụng cũng như là maintain nó, đặc biệt là khi tiến hành mở rộng ứng dụng. Bạn càng thêm mới nhiều chức năng, thì code của bạn càng nhiều thêm.

Tạo một cấu trúc phù hợp với ứng dụng của bạn ngày từ khi bắt tay vào làm, để cấu trúc đó có thể thích ứng với mọi yêu cầu thay đổi trong tương lai luôn là vấn đề đau đầu với những nhà lập trình viên, đặc biệt là nó không được quản lý đúng cách. Để giúp cho vấn đề này trở nên dễ dàng hơn, NestJs đã được ra đời.

NestJs được xây dựng để loại bỏ những đoạn code vô tổ chức và cung cấp cho ứng dụng Node một cấu trúc hợp lý. Dựa trên nền tảng của Angular, NestJs được xây dựng với TypeScript và sử dụng Express.js. Điều này khiến nó tương thích nhanh với đa số những phần mềm trung gian.

Trong bài viết này, tôi xin giới thiệu với các bạn đọc về NestJS cũng như là hướng dẫn các bạn làm quen với nó. Bạn sẽ được biết cách để cài đặt framework trên máy cá nhân của mình. Trong quá trinh thực hiện điều này, hãy bắt tay làm với một ví dụ đơn giản (học đi đôi với hành mà) để hiểu rõ hơn về framwork này. Bài toán của chúng ta sẽ ứng dụng tìm kiếm, thêm mới, .. sách vào thư viện.

## Yêu cầu

- Kiến thức về Javascript cũng như là TypeScript sẽ giúp ích rất nhiều cho bạn trong bài viết này.
- Có kinh nghiệm làm việc với Agular sẽ giúp bạn dễ đọc hiểu hơn, nhưng chưa có cũng không sao, chúng ta sẽ cùng nhau nghiên cứu.
- Cài đặt Node và npm trên máy là điều không thể không làm.

## Xây dựng project bằng NestJs framework

## Controllers

Mô hình MVC không còn quá lạ lẫm với chúng ta, và Controller là một phần quan trọng trong mô hình này. Cũng giống như mọi framework khác, Controller trong NestJs chịu trách nhiệm xử lý mọi request đến và trả về response cho phía client. 

NestJs đươc cấu trúc theo cách mà cơ chế định tuyến có thể cho phép Controller nào xử lý một yêu cầu cụ thể.

Dưới đây là một ví dụ về Controller

```
// users.controller.ts 

import { Controller, Get } from '@nestjs/common';

	@Controller('users')
	export class UsersController {
		@Get()
			findAll() { 
				return 'This will return all the users';
		}
	}
```

prefix _users_, khi có request GET /users từ phía client lên Controller, thì Controller sẽ tiếp nhận và xử lý lấy tất cả users trong cơ sở dữ liệu và trả về cho phía client thông qua hàm findAll(). Ngoài method GET ra thì NestJs cũng hỗ trợ HTTP method khác như PUT, POST, DELETE.

- Khi tạo mới một Controller, nó cần được định nghĩa trong module trước khi NestJs có thể nhận ra được nó. Module đó có tên là ApplicationModule.

## Providers

Như đã nói tới ở phần mở đâu, NestJs dựa vào AngularJS để làm nền tảng phát triển. Cũng giống như Angular, chúng ta có thể dễ dàng tạo ra services và sử dụng nó trong Controllers hay trong các services khác.

- Services trong NestJs đơn thuần chỉ là một Class Javascript bình thường, bắt đầu với từ khóa _@Injectable()_ ở trên cùng.

Ví dụ về một services:

```
 // users.service.ts

import { Injectable } from '@nestjs/common';
import { User } from './interfaces/user.interface';

@Injectable()
export class UsersService {
	private readonly users: User[] = [];

	create(user: User) { 
	this.users.push(user);   }

	findAll(): User[] {
		return this.users;
	}
}
```
