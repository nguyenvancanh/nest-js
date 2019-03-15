# Nest-js

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
		this.users.push(user);   
	}

	findAll(): User[] {
		return this.users;
	}
}
```

Trong ví dụ trên, chúng ta đã định nghĩa 2 method là create() và findAll() dùng để tạo mới một user cũng như là trả về tất cả người dùng đang có trong DB.

## Modules

Modules cũng là một phần quang trọng của framewordk NestJs. Mỗi ứng dụng NestJs nên có nhiều hơn một module. Mỗi modules thì được bắt đầu bằng @Modules. Xem ví dụ dưới đây

```
import { Module } from '@nestjs/common';
import { UsersController } from './users.controller.ts';
import { UsersService } from './users.service.ts';

@Module({
  controllers: [UsersController],
  providers: [UsersService]
})

export class UsersModule {}
```

Trong ví dụ này,chúng ta đã export một class là _UsersModule_ bên trong nó bao gồm cả UsersController và UsersService. Sau khi export thì chúng ta có thể dễ dàng sử dụng Module này ở bất kỳ đâu mà chúng ta muốn

```
...
import { UsersModule } from './users/users.module';

@Module({
  ...
})

export class AppModule { }
```

Trên đây là một vài khái niệm cơ bản của framework NestJs, bây giờ chúng ta sẽ đi vào phần thực hành

## Cài đặt NestJs

Cài đặt Nest CLI bằng lệnh

```
npm i -g @nestjs/cli
```

Tạo mới một project NestJS băng dòng lệnh

```
nest new bookstore
```

Chuyển root dir vào thư mục project và start npm

```
// change directory
cd bookstore-nest


// start the application
npm run start
```

Sau khi start npm, [http://localhost:3000/](http://localhost:3000/) để kiểm tra xem framework của bạn đã được start hay chưa và đảm bảo rằng việc cài đặt của bạn không gặp vấn đề gì.

## Tạo Module đầu tiên

```
nest generate module books
```

Câu lệnh này sẽ tạo mới một folder với tên là books ở trong /src và trong folder đó sẽ có một file với tên _books.module.ts_ có default code như sau

```
// ./src/books/books/module.ts

import { Module } from '@nestjs/common';
@Module({})
export class BooksModule {}
```
Và đương nhiên, command trên cũng đã khai báo file vừa tạo ở trong file _app.module.ts_ cho chúng ta rồi.

## Tạo route

```
nest generate controller books
```

Câu lệnh này sẽ tạo cho bạn một Controller bên trong thư mục books. Từ đầu tới giờ,chúng ta chưa hết connect tới database nào cả. tạm thời chúng ta hãy tạo một bộ dữ liệu giả lập trước. Để làm được điều này, trước tiên, hãy tạo một thư mục con bên trong /src với tên là _mocks_, bên trong thưc mục này tạo file _books.mock.ts_ với nội dung

```
// ./src/mocks/books.mock.ts
export const BOOKS = [
    { id: 1, title: 'First book', description: "This is the description for the first book", author: 'Olususi Oluyemi' },
    { id: 2, title: 'Second book', description: "This is the description for the second book", author: 'John Barry' },
    { id: 3, title: 'Third book', description: "This is the description for the third book", author: 'Clement Wilfred' },
    { id: 4, title: 'Fourth book', description: "This is the description for the fourth book", author: 'Christian nwamba' },
    { id: 5, title: 'Fifth book', description: "This is the description for the fifth book", author: 'Chris anderson' },
    { id: 6, title: 'Sixth book', description: "This is the description for the sixth book", author: 'Olususi Oluyemi' },
];
```

## Khai báo Services

Chạy câu lệnh

```
nest generate service books
```
sẽ tạo cho chúng ta file _books.service.ts_ trong thư mục /src/books

## Tạo method Get books

Mở file service bên trên vừa được khởi tạo và paste dòng code này vào

```
//  ./src/books/books.service.ts

  import { Injectable, HttpException } from '@nestjs/common';
  import { BOOKS } from '../mocks/books.mock';

  @Injectable()
  export class BooksService {
      books = BOOKS;

      getBooks(): Promise<any> {
          return new Promise(resolve => {
              resolve(this.books);
          });
      }
      getBook(bookID): Promise<any> {
          let id = Number(bookID);
          return new Promise(resolve => {
              const book = this.books.find(book => book.id === id);
              if (!book) {
                  throw new HttpException('Book does not exist!', 404);
              }
              resolve(book);
          });
      }
  }
``` 

Đầu tiên là bạn import một số module cần thiết từ NestJs và BOOKS từ mocks data bạn tạo ở bước trên. Tiếp theo là tạo 2 methos getBooks() và getBook(). Method getBooks() trả về tất cả books có trong dữ liệu của bạn, còn method getBook() thì sẽ trả về 1 giá trị với bookId được truyền vào.

## Thêm mới sách

Thêm method addBook() vào file service bên trên, phía dưới hàm getBook()

```
 addBook(book): Promise<any> {
        return new Promise(resolve => {
            this.books.push(book);
            resolve(this.books);
        });
    }
```

## Xóa sách

Tương tự như trên, thêm method deleteBook() vào 

```
//  ./src/books/books.service.ts

import { Injectable, HttpException } from '@nestjs/common';
import { BOOKS } from '../mocks/books.mock';
@Injectable()
export class BooksService {
    books = BOOKS;
    ...
    deleteBook(bookID): Promise<any> {
        let id = Number(bookID);
        return new Promise(resolve => {
            let index = this.books.findIndex(book => book.id === id);
            if (index === -1) {
                throw new HttpException('Book does not exist!', 404);
            }
            this.books.splice(1, index);
            resolve(this.books);
        });
    }
}
```

## Inject Service vào trong Controller

Mở file controller lên và thêm đoạn code sau

```
// ./src/books/books.controller.ts

import { Controller, Get, Param, Post, Body, Query, Delete } from '@nestjs/common';
import { BooksService } from './books.service';
import { CreateBookDTO } from './dto/create-book.dto';

@Controller('books')
export class BooksController {
    constructor(private booksService: BooksService) { }

    @Get()
    async getBooks() {
        const books = await this.booksService.getBooks();
        return books;
    }

    @Get(':bookID')
    async getBook(@Param('bookID') bookID) {
        const book = await this.booksService.getBook(bookID);
        return book;
    }

    @Post()
    async addBook(@Body() createBookDTO: CreateBookDTO) {
        const book = await this.booksService.addBook(createBookDTO);
        return book;
    }

    @Delete()
    async deleteBook(@Query() query) {
        const books = await this.booksService.deleteBook(query.bookID);
        return books;
    }
}
```

Ở trong file Controoler bạn để ý rằng chúng ta có sử dụng CreateBookDTO, nó là một object để chuyển đổi dữ liệu, hiểu đơn giản là một class được tạo ra để validate giá trị của input đầu vào của bạn. Được định nghĩa như sau

```
// ./src/books/dto/create-book.dto.ts

export class CreateBookDTO {
    readonly id: number;
    readonly title: string;
    readonly description: string;
    readonly author: string;
}
```

Quay lại file Module một chút và update lại code

```
// ./src/books/books.module.ts

import { Module } from '@nestjs/common';
import { BooksController } from './books.controller';
import { BooksService } from './books.service';
@Module({
  controllers: [BooksController],
  providers: [BooksService]
})
export class BooksModule {}
```

Chạy lại 

```
npm run start
```

và kiểm tra kết quả trên web. chúc m
