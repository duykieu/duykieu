---
title: Giới thiệu design pattern trong Javascript
date: 2021-01-02 20:00:00
tags:
  - Design Pattern
  - Javacript
categories:
  - [Design pattern, Javascript]
---

## Giới thiệu

Là một JS developer, bạn luôn phấn đấu tìm cách viết code sao cho sạch, khỏe, và dễ bảo trì. Bạn giải quyết những thách thức mặc dù là duy nhất nhưng không yêu cầu sử dụng một giải pháp duy nhất. Đôi khi, có thể bạn thất rằng mình đang viết code trông giống như trước đây mình đã viết rồi và giờ đây dùng để giải quyết một vấn đề hoàn toàn khác. Có thể bạn chưa biết, đó chính là **design pattern**. Design pattern là những giải pháp tái sử dụng code thường xảy ra trong các vấn đề thiết kế phần mềm.

Trong suốt thời gian tồn tại của bất kỳ ngôn ngữ nào, rất nhiều giải pháp tái sử dụng code được tạo ra và test bởi một số lượng lớn các lập trình viên từ cộng đồng của ngôn ngữ đó. Đó là bởi vì sự kết hợp kinh nghiệm của các lập trình viên chứng minh rằng có những giải pháp đó có ích bởi vì chúng giúp chúng ta viết code tối ưu hơn đồng thời giải quyết vấn đề trong tầm tay.

Những lợi ích của design patterns:

- **Chúng chứng minh các giải pháp**: Bởi vì design pattern thường được sử dụng bởi rất nhiều lập trình viên, và chắc chắn rằng chúng làm việc tốt. Không chỉ vậy, bạn còn chắc chắn rằng chúng đã được sửa lại nhiều lần và có thể còn được tối ưu hóa liên tục.
- **Dễ dàng tái sử dụng**: Design pattern ghi lại giải pháp tái sử dụng có thể được chỉnh sửa để giải quyết nhiều bài toán cụ thể vì chúng không gắn liền với một vấn đề cụ thể.
- **Tính biểu cảm**: Các design pattern có thể giải thích một vấn đề lớn một cách gọn nhẹ.
- **Tính kết nối**: Khi các lập trình viên đã quen với các design pattern, họ có thể dễ dàng kết nối trao đổi với nhau hơn trong việc giải quyết các vấn đề.
- **Hạn chế refactor code**: Nếu một ứng dụng được viết với tư tưởng design pattern, thường thì bạn không cần phải refactor code bởi vì nó được áp dụng đúng design pattern và vấn đề được giải quyết bằng một giải pháp đã được tối ưu.
- **Code ít hơn**: Bởi vì design pattern thường gọn nhẹ và là những giải pháp tối ưu, chúng thường yêu cầu ít code hơn các giải pháp khác.

Bây giờ trước khi vào chi tiết các design pattern, hãy nhìn lại một số điểm cơ bản của Javascript:

## Sơ lược về lịch sử Javascript

Javascript là một trong những ngôn ngữ phổ biến nhất trong lập trình web ngày nay. Bạn đầu nó được thiết kế như một dạng keo kết dính để hiển thị các element trong trình duyệt, được xem như ngôn ngữ kịch bản phía client cho một trong những trình duyệt đầu tiên của thế giới, gọi là Netscape Navigator, nó chỉ có thể hiển thị trang HTML tĩnh tại một thời điểm. Có thể bạn đang nghĩ đúng, ý tưởng về một ngôn ngữ kịch bản như vậy đã dẫn đến cuộc chiến trình duyệt giữa các ông lớn trong ngành phát triển trình duyệt hồi đó, chẳng hạn như Netscape Communication (ngày nay là Mozilla), Microsoft và các công ty khác.

Mỗi hãng đều muốn triển khai loại ngôn ngữ kịch bản này của riêng họ, vì vậy Netscape tạo ra Javascript, Microsoft tạo ra JScript,... Bạn có thể tưởng tượng, khi khác nhau giữa những loại script này khác nhau thế nào, vì vậy phát triển web được thực hiện cho từng trình duyệt. Và cái gì đến cũng đến, mọi người cần một _chuẩn_, một giải pháp cross-browser, hợp nhất quá trình phát triển và đơn giản hóa việc tạo ra các trang web. Và họ nghĩ ra ECMAScript.

ECMAScript là một chuẩn ngôn ngữ kịch bản đặc thù mà tất cả các trình duyệt hiện đại cố gắng hỗ trợ, và lại có nhiều khách triển khai của ECMAScript. Nổi tiếng nhất là cách triển khai trong bài viết này, vâng Javascript. Từ khi được phát hành lần đầu, ECMAScript đã được chuẩn hóa nhiều lần trong mỗi phiên bản. Các trình duyệt vẫn chưa hoàn toàn hỗ trợ ES6 cho tới thời điểm tôi viết bài này và vẫn phải chuyển đổi xuống ES5 để được hỗ trợ đầu đủ.

## Javascript là gì ?

Để tìm hiểu được nội dung của bài viết này, ta cần biết những đặc điểm quan trọng của ngôn ngữ này. Nếu ai đó hỏi bạn Javascript là gì, có thể bạn sẽ trả lời như sau:

> Javascript là một ngôn ngữ thông dịch, nhẹ, hướng đối tượng với first-class function, thường được biết đến như một ngôn ngữ kịch bản phổ biến nhất dành cho web.

Định nghĩa trên đây cho biết Javascript sử dụng ít bộ nhớ, dễ triển khai, dễ học, cú pháp tương tự C++ và Java. Nó là ngôn ngữ kịch bản, nghĩa là được thông dịch thay vì biên dịch. Hỗ trợ lập trình hướng thủ tục, hướng đối tượng và lập trình hàm, làm cho nó vô cùng linh hoạt với các lập trình viên.

Cho đến nay, ta đã xem xét tất cả những đặc điểm nghe giống như các ngôn ngữ khác, giờ hãy xem những điểm cụ thể nào mà Javascript khác với các ngôn ngữ khác. Tôi sẽ chỉ liệt kê một vài đặc điểm đáng được quan tâm đặc biệt.

### Javscript hỗ trợ first-class function.

Đặc điểm này gây cho tôi khá nhiều khó khăn khi mới bắt đầu với Javscript, khi background của tôi là C/C++. Javascript xem function như first-class citizens, có nghĩa rằng bạn có thể truyền một hàm vào một hàm khác như một tham số như các biến khác.

```javascript
// Chúng ta truyền vào hàm biến cb như một tham số,
// callback này sẽ được chạy trong hàm
function performOperation(a, b, cb) {
  var c = a + b;
  cb(c);
}

performOperation(2, 3, function (result) {
  // in ra 5
  console.log("The result of the operation is " + result);
});
```

### Javascript là Prototype-based

Cũng như các ngôn ngữ hướng đối tượn khác, Javascript hỗ trợ các đối tượng, và một trong các thuật ngữ đầu tiên xuất hiện trong suy nghĩ về đối tượng là các _class_(lớp) và _inheritance_(tính thừa kế). Đây là điểm có chút khó khăn, khi ngôn ngữ không hỗ trợ class (bản chất) mà sử dụng một cách khác gọi là prototype-based hoặc instance-based.

Hiện nay trong ES6, thuật ngữ class chính thức được giới thiệu, nhưng trình duyệt vẫn chưa hỗ trợ đầy đủ. Rất quan trọng để ghi nhớ, tuy nhiên, thậm chí khi "class" được giới thiệu thì Javascript, bản chất vẫn thực hiện thừa kế bằng prototype-based.

Lập trình prototype-based là một phong cách thực hiện hướng đối tượng mà hành vi thừa kế được thực hiện thông qua một quá trình tái sử dụng một đối tượng thông qua prototype. Chúng ta sẽ đào sâu hơn về vấn đề này khi vào phần design pattern của bài viết này, vì đặc điểm này sử dụng rất nhiều trong Javascript design patterns.

### Javascript Event Loop

Nếu bạn có kinh nghiệm với Javascript chắc hẳn bạn đã quen thuộc với thuật ngữ **callback**. Với những ai chưa quen với thuật ngữ này, một hàm callback là một hàm được truyền vào hàm khác như một tham số (hãy nhớ, Javascript xem các hàm như là first-class citizens), hàm này được chạy sau khi một sự kiện được thực thi. Nó thường được dùng để đăng ký các sự kiện như click chuột hoặc gõ bàn phím.

![Event Loop trong Javascript](https://uploads.toptal.io/blog/image/125781/toptal-blog-image-1522333483007-ac9070c74c6ae7747cb2fa551667d8e5.png)

Mỗi lần một sự kiện được lắng nghe bởi một listener được thực thi, một message được gửi vào hàng đợi, hàng đơi này sẽ được thực hiện tuần từ (đồng bộ) theo cách FIFO (first in first out). Đây được gọi là Event Loop.

Mỗi một message trong hàng đợi có một hàm liên kết với nó. Khi một message được xử lý, runtime sẽ thực thi hàm một cách hoàn chỉnh trước khi xử lý message khác. Nếu một hàm lại gọi đến một hàm khác chúng sẽ được xử lý tất cả trước khi đến với message tiếp theo.

    while (queue.waitForMessage()) {
        queue.processNextMessage();
    }

Phương thức `queue.waitForMessage()` sẽ chờ đợi một cách "đồng bộ" các message mới. Một message được xử lý với stack riêng biệt của nó cho đến khi stack trống. Khi hoàn thành, một message khác được xử lý trong queue nếu có tồn tại.

Có thể bạn đã nghe qua Javascript có tính non-blocking, có nghĩa là khi một hàm asynchronous được thực thi, chương trình vẫn có thể chạy các tiến trình khác như nhận các giá trị mà nhập vào từ người dùng, trong khi chờ các hàm asynchronous hoàn thành, không block main thread. Đây là tính năng rất hữu ích của Javascript và nó có thể phải được viết bằng cả một bài; tuy nhiên, đây không thuộc phạm vi của bài viết này.

## Design pattern là gì?

Như tôi đã nói trước đó, design pattern là các giải pháp tái sử dụng cho những vấn đề phổ biến trong thiết kế phần mềm. Hãy nói về một số loại design pattern.

### Proto-pattern

Làm thế nào người ta tạo ra pattern?. Thử nghĩ thế này, bạn nhận ra rằng một vấn đề thường xuyên xảy ra, và bạn có giải pháp của riêng bạn để giải quyết vấn đề đó, và cách của bạn chưa được công nhận và giải thích trên toàn cầu. Bạn sử dụng giải pháp này mỗi khi bạn gặp vấn đề tương tự, bạn nghĩ rằng nó có thể tái sử dụng và cộng đồng lập trình có thể nhận lợi ích từ việc sử dụng nó.

Vậy nó có ngay lập tức trở thành một pattern hay không?. May mắn thay, không. Thông thường một người có thể có các phương pháp viết code tốt và chỉ đơn giản nhầm lẫn một thứ gì đó với design pattern, thực tế, nó không phải design pattern.

Làm thế nào bạn biết khi nào những gì bạn ngữ thật sự trở thành một design pattern?

Bằng cách nhận được ý kiến từ các lập trình viên khác, bằng cách biết được quá trình một design pattern được tạo ra, và bằng cách chính bạn làm quen với các design pattern đã tồn tại. Có một giai đoạn mà một pattern phải trải qua trước khi trở thành một pattern chính thức. Đây được gọi là proto-pattern.

A proto-pattern là một pattern nếu nó vượt qua một thời kỳ kiểm định bởi rất nhiều lập trình viên, rất nhiều hoàn cảnh khi mà pattern chứng minh được rằng nó hữu ích và cho ra kết quả chính xác. Có rất nhiều công việc và tài liệu được viết ra trước khi trở thành một pattern chính thức được đón nhận bởi cộng đồng.

### Anti-pattern

Một design pattern đại diện cho code tốt, anti-pattern đại diện cho code tệ.

Một ví dụ về anti-pattern là việc chỉnh sửa prototype của đối tượng `Object`. Hầu hết tất cả các đối tượng trong Javascript sẽ thừa kế từ đối thượng `Object` (Hãy nhớ rằng Javascript thừa kế dựa trên prototype), vì vậy hãy tưởng tượng bạn sửa prototype của đối tượng này dẫn đến tất cả các đối tượng được thừa kế từ `Object` sẽ có thuộc tính này và rồi, **thảm họa chỉ chờ đợi ngày xảy ra**.

Một ví dụ khác, tương tự như ví dụ trên, đó là chỉnh sửa các đối tượng mà bạn không sở hữu. Đó là việc bạn ghi đè một hàm được sử dụng trong nhiều hoàn cảnh khác nhau trong toàn bộ ứng dụng. Nếu bạn làm việc với một team lớn, thử tưởng tượng những rắc rối nó gây ra; bạn nhanh chóng dính phải lỗi đặt tên va chạm, triển khai không tương thích và ác mộng bảo trì.

Tương tự như việc học được những điều tốt, thì học những điều xấu cũng quan trọng không kém. Bằng cách này bạn có thể nhận thức và tránh mắc lỗi phía trước:

## Phân loại design pattern

Design pattern có thể phân loại theo nhiều cách, những phổ biến nhất như sau:

- Creational Design Patterns
- Structural design patterns
- Behavioral design patterns
- Concurrency design patterns
- Architectural design patterns

### Creational Design Patterns

Các pattern này giải quyết vấn đề khởi tạo đối tượng để tối ưu hóa việc khởi tạo đối tượng khi so sánh với cách cơ bản. Một hình thức khởi tạo đối tượng có thể ảnh hưởng đến vấn đề thiết kế hoặc thêm tính phức tạp vào thiết kế. Các design pattern trong khởi tạo giải quyết vấn đề này bằng cách kiểm soát việc khởi tạo đối tượng. Một vài design pattern trong nhóm này gồm:

- Phương thức factory
- Abstract factory
- Builder
- Prototype
- Singleton

### Structural design patterns

Các pattern này giải quyết vấn đề quan hệ giữa các đối tượng. Chúng đảm bảo rằng nếu một phần nào của hệ thống thay đổi, toàn bộ hệ thống sẽ không ảnh hưởng, không cần thay đổi theo nó. Các pattern phổ biến:

- Adapter
- Bridge
- Composite
- Decorator
- Facade
- Flyweight
- Proxy

### Behavioral design patterns

Loại pattern này nhận biết, thực hiện và cải tiến sự giao tiếp giữa các đối tượng trong hệ thống. Chúng giúp đảm bảo rằng các thành phần khác nhau của hệ thống được đồng bộ thông tin. Các pattern phổ biến:

- Chain of responsibility
- Command
- Iterator
- Mediator
- Memento
- Observer
- State
- Strategy
- Visitor

### Concurrency Design Patterns

Loại này giải quyết vấn đề multi-thread trong lập trình. Một vài pattern phổ biến:

- Active object
- Nuclear reaction
- Schedule

### Architectural Design Patterns

Các design pattern dùng trong thiết kế kiến trúc dự án:

- MVC (Model - View - Controller)
- MVP (Model - View - Presenter)
- MVVM (Model - View - ViewModel)

Trong phần tiếp theo của bài viết, chúng ta sẽ đi sâu hơn một vài loại design pattern đã nói ở trên với các ví dụ để hiểu kỹ hơn

## Các ví dụ về design pattern

Mỗi một design pattern đại diện cho một loại giải pháp cụ thể cho một vấn đề cụ thể. Không có một tập các pattern chung nào là phù hợp hoàn toàn. Chúng ta cần học khi nào một pattern cụ thể sẽ chứng minh là có ích và khi nào nó sẽ cung cấp giá trị thực sự. Khi ta đã quen với các pattern và các hoàn cảnh mà nó phù hợp để sử dụng, ta có thể dễ dàng quyết định khi nào một pattern phù hợp cho vấn đề đặt ra.

Hãy nhớ, áp dụng sai pattern có thể dẫn đến các hiệu ứng không mong muốn như code complexity không cần thiết, chi phí hiệu suất không phù hợp hoặ thậm chí sinh ra một anti-pattern mới.

Đây là tất cả những điều quan trọng cần phải nghĩ kỹ trước khi áp dụng pattern vào code chúng ta. Chúng ta sẽ xem xét một vài pattern mà bản thân tôi thấy có ích và tin rằng bất kỳ một senior nào cũng cần phải quen thuộc.

### Constructor pattern

Khi nghĩ về các ngôn ngữ hướng đối tượng cổ điển, một constructor là một hàm đặc biệt trong class khởi tạo đối tượng với một số thuộc tính mặc định.

Có 3 cách khởi tạo đối tượng phổ biến trong Javacript:

```javascript
const instance = {};
//hoặc
const instance = Object.create(Object.prototype);
//hoặc
const instance = new Object();
```

Sau khi khởi tạo đối tượng, có 4 cách để thêm thuộc tính vào các đối tượng. Chúng là:

```javascript
//Hỗ trợ từ ES3
instance.key = "A key's value";
instance["key"] = "A key's value";
//Từ ES5
//Thêm một thuộc tính đơn
Object.defineProperty(instance, "key", {
  value: "A key's value",
  writable: true,
  enumerable: true,
  configurable: true,
});
//Thêm nhiều thuộc tính
Object.defineProperty(instance, {
  firstKey: {
    value: "First key's value",
    writable: true,
  },
  secondKey: {
    value: "Second key's value",
    writable: false,
  },
});
```

Cách phổ biến nhất là dùng một cặp dấu ngoặc nhọn rồi sau đó khi thêm thuộc tính dùng dấu chấm kèm với key. Bất kỳ ai có kinh nghiệm với Javascript đều đã dùng như vậy.

Trước đó chúng ta đã nói rằng JS bản chất không hỗ trợ class nhưng nó hỗ trợ constructor thông qua từ khóa `new` đi liền trước hàm. Bằng cách này ta có thể dùng các hàm như một constructor và khởi tạo các thuộc tính cho đối tượng tương tự như thực hiện với constructor của các ngôn ngữ cổ điển.

```javascript
// định nghĩa constructor cho các đối tượng của Person
function Person(name, age, isDeveloper) {
  this.name = name;
  this.age = age;
  this.isDeveloper = isDeveloper || false;

  this.writesCode = function () {
    console.log(
      this.isDeveloper
        ? "This person does write code"
        : "This person does not write code"
    );
  };
}

var person1 = new Person("Bob", 38, true);

var person2 = new Person("Alice", 32);

person1.writesCode();
person2.writesCode();
```

Tuy nhiên, vẫn còn chỗ để cải tiến. Nếu bạn nhớ, tôi đã đề cập trước đây rằng Javascript sử dụng prototype-based để thừa kế. Vấn đề của cách vừa rồi là phương thức `writeCode` sẽ được định nghĩa lại trên rất cả các đối tượng được khởi tạo từ constructor `Person`. Chúng ta có thể tránh việc này bằng cách đặt phương thức vào prototype của hàm:

```javascript
// Định nghĩa constructor
function Person(name, age, isDeveloper) {
  this.name = name;
  this.age = age;
  this.isDeveloper = isDeveloper || false;
}

// Mở rộng prototype của hàm constructor Person
Person.prototype.writesCode = function () {
  console.log(
    this.isDeveloper
      ? "This person does write code"
      : "This person does not write code"
  );
};

var person1 = new Person("Bob", 38, true);

var person2 = new Person("Alice", 32);

person1.writesCode();
person2.writesCode();
```

Bây giờ tất cả các đối tượng của hàm constructor `Person` có thể truy cập vào phương thức được share là `writesCod()e`.

### Module pattern

Với đặc thù của mình, Javascript không bao giờ ngừng tạo ra những ngạc nhiên. Một điều đặc biệt khác đối với Javascript là nó không hỗ trợ sửa đổi truy cập (access modify). Trong các ngôn ngữ OOP cổ điển, ta định nghĩa class và quyết định quyền truy cập cho các thành viên của nó. Trong khi Javascript không hỗ trợ class, đồng thời cũng không hỗ trợ sửa đổi truy cập, và các lập trình viên JS phải tìm cách để bắt chước hành vi này khi cần thiết.

Trước khi đi vào module pattern, hãy nói về khái niệm closure. Một closure là một hàm được truy cập vào scope của hàm cha, thậm chí khi hàm cha đã đóng (return). Chúng giúp ta bắt chước hành vi của các access modifier thông qua scope. Hãy xem:

```javascript
// Chúng ta sử dụng immediately invoked function expression
// để tạo một biến private (counter)
var counterIncrementer = (function () {
  var counter = 0;

  return function () {
    return ++counter;
  };
})();

// In ra 1
console.log(counterIncrementer());
// In ra 2
console.log(counterIncrementer());
// In ra 3
console.log(counterIncrementer());
```

Bạn có thể thấy, bằng cách sử dụng IIFE, ta đã gắn biến `counter` vào một hàm _đã được chạy và đã đóng_ nhưng vẫn có thể truy cập bởi hàm con để tăng nó lên. Bởi vì ta không thể truy cập `counter` từ bên ngoài scope của hàm. Ta làm cho nó private thông qua scope.

Sử dụng closure, ta có thể tạo ra các cái gọi là private và public. Đây gọi là **module** và rất có ích khi bạn muốn ẩn đi phần nào đó của đối tượng và chỉ để lộ ra phần giao diện cho người dùng module. Hãy xem:

```javascript
// thông qua closure ta chỉ hiện ra các public API
// quản lý các đối tượng mảng private
var collection = (function () {
  // priate
  var objects = [];

  // public
  return {
    addObject: function (object) {
      objects.push(object);
    },
    removeObject: function (object) {
      var index = objects.indexOf(object);
      if (index >= 0) {
        objects.splice(index, 1);
      }
    },
    getObjects: function () {
      return JSON.parse(JSON.stringify(objects));
    },
  };
})();

collection.addObject("Bob");
collection.addObject("Alice");
collection.addObject("Franck");
// In ra ["Bob", "Alice", "Franck"]
console.log(collection.getObjects());
collection.removeObject("Alice");
// In ra ["Bob", "Franck"]
console.log(collection.getObjects());
```

Điểm đáng giá nhất mà pattern này đem đến là việc phân chia rõ ràng những phần public và private của một đối tượng, concept mà đã rất quen thuốc với các lập trình viên có background OOP cổ điển.

Tuy nhiên, không có gì là hoàn hảo. Khi bạn muốn ẩn hiện một biến nào đó, bạn buộc phải sửa code ở tất cả những nơi sử dụng đến biến này bởi vì bản chất khác nhau của việc truy cập public và private. Thêm nữa, các phương thức được thêm vào đối tượng sau khi khởi tạo không thể truy cập vào các biến private.

### Revealing Module Pattern

Pattern này là một bản cải tiến của module pattern được minh họa trên đây. Điểm khác nhau chính đó là chúng ta viết toàn bộ logic của object bên trong private scope của module, và sau đó đơn giản là trả về một phần mà ta muốn public. Ta cũng có thể thay đổi tên của biến private khi mapping biến private đến biến public.

```javascript
const namesCollection = (function () {
  // Biến private
  const objects = [];

  function addObject(object) {
    objects.push(object);
  }

  function removeObject(object) {
    var index = objects.indexOf(object);
    if (index >= 0) {
      objects.splice(index, 1);
    }
  }

  function getObjects() {
    return JSON.parse(JSON.stringify(objects));
  }

  // Biến public
  return {
    addName: addObject,
    removeName: removeObject,
    getNames: getObjects,
  };
})();

namesCollection.addName("Bob");
namesCollection.addName("Alice");
namesCollection.addName("Franck");
// In ra ["Bob", "Alice", "Franck"]
console.log(namesCollection.getNames());
namesCollection.removeName("Alice");
// In ra ["Bob", "Franck"]
console.log(namesCollection.getNames());
```

Revealing pattern là một trong số ít nhất ba cách thực hiện module pattern. Sự khác nhau giữa revealing module và những cách khác đó là _các biến public được tham chiếu như thế nào_. Và kết quả là reaveal module pattern rất dễ dàng để chỉnh sửa; tuy nhiên, nó khá mong manh trong một số trường hợp, như sử dụng các đối tượng của reveal module pattern như là prototype trong chuỗi prototype. Các vấn đề sẽ xảy ra:

1. Nếu ta có một hàm private được tham chiếu bởi một hàm public, ta không thể ghi đè hàm public, bởi vì hàm private tiếp tục tham chiếu đến cách hàm private, dẫn đến bug trong hệ thống.
2. Nếu ta có một biến public trỏ đến một biến private và cố gắng ghi ghé biến public từ bên ngoài module, các hàm khác vẫn tham chiếu đến giá trị private của biến, cũng dẫn đến bug

### Singleton pattern

Singleton pattern được dùng trong trường hợp bạn cần duy nhất một đối tượng. Ví dụ, bạn cần một đối tượng chứa cấu hình của hệ thống. Trong trường hợp này, không cần thiết để tạo ra một đối tượng mới khi cần sử dụng đến đối tượng này ở đâu đó trong hệ thống.

```javascript
const singleton = (function () {
  // Giá trị private singleton được khởi tạo chỉ một lần
  const config;

  function initializeConfiguration(values) {
    this.randomNumber = Math.random();
    values = values || {};
    this.number = values.number || 5;
    this.size = values.size || 10;
  }

  // Ta export phương thức trung tâm để nhận giá trị của singleton
  return {
    getConfig: function (values) {
      // Khởi tạo giá trị của singleton một lần duy nhất
      if (config === undefined) {
        config = new initializeConfiguration(values);
      }

      // và trả về cùng một giá trị config khi được truy cập
      return config;
    },
  };
})();

var configObject = singleton.getConfig({ size: 8 });
// In ra number: 5, size: 8, randomNumber: someRandomDecimalValue
console.log(configObject);
var configObject1 = singleton.getConfig({ number: 8 });
// In ra number: 5, size: 8, randomNumber: same randomDecimalValue as in first config
console.log(configObject1);
```

Như bạn thấy trong ví dụ, random number cũng như giá trị của config là không đổi.

Hãy ghi nhớ điểm quan trọng nhất là điểm truy cập để lấy giá trị singleton là duy nhất. Nhược điểm của pattern này là rất khó để test

### Observer Pattern

Observer pattern là một công cụ hữu ích trong trường hợp ta cần cải tiền kết nối giữa các thành phần trong hệ thống theo một cách tối ưu. Nó gắn kết những liên kết lỏng lẻo giữa các đối tượng.

Có nhiều phiên bản của pattern này, nhưng cơ bản sẽ có hai thành phần chính là subject và observers.

Subject xử lý tất cả các hoạt động liên quan đến một chủ đề nhất định mà observers đã đăng ký. Các hoạt động này đăng ký một observer vào một chủ đề nhất định, bỏ đăng ký khỏi chủ đề và thông báo cho observer các sự kiện đã được phát hành.

Tuy nhiên có một phiên bản được gọi là publisher/subcriber pattern mà tôi sẽ sử dụng làm ví dụ trong phần này. Sự khác nhau chính so với observer pattern cổ điển đó là publisher/subcriber đó là publisher/subcriber pattern sẽ liên kết chặt chẽ hơn.

Trong observer pattern, subject giữ tham chiếu đến subcriber và gọi các phương thức trực tiếp từ chính các đối tượng, trong khi đó, publisher/subcriber patterns, chúng ta có các kênh được chạy như một cầu kết nối giữa subcriber và publisher. Publisher fire một event và đơn giản là thực thi hàm callback được gửi cho event đó.

Tôi sẽ làm một ví dụ cơ bản về publisher/subcriber pattern, cho những ai quan tâm về observer pattern cổ điển, tôi sẽ sớm có bài viết chi tiết về observer pattern, hoặc các bạn cũng có thể dễ dàng tìm online.

```javascript
// chúng ta gửi vào một đối tượng container để quản lý subcribtions và publishings
(function (container) {
  // id đại diện cho một subscription duy nhất đến một chủ đề
  const id = 0;

  // chúng ta đăng ký đến một chủ đề nhất định bằng cách gửi vào
  // một hàm callback để thực thi khi sự kiện xảy ra
  container.subscribe = function (topic, f) {
    if (!(topic in container)) {
      container[topic] = [];
    }

    container[topic].push({
      id: ++id,
      callback: f,
    });

    return id;
  };

  // mỗi subscription có id riêng của nó sẽ được dùng
  // để xóa một subscriber khỏi topic nào đó
  container.unsubscribe = function (topic, id) {
    const subscribers = [];
    for (const subscriber of container[topic]) {
      if (subscriber.id !== id) {
        subscribers.push(subscriber);
      }
    }
    container[topic] = subscribers;
  };

  container.publish = function (topic, data) {
    for (const subscriber of container[topic]) {
      // khi thực thi một callback, sẽ có ích khi đọc
      // tài liệu để biết những tham số nào sẽ được
      // truyền vào callback khi đối tượng fire event
      subscriber.callback(data);
    }
  };
})(publisherSubscriber);

var subscriptionID1 = publisherSubscriber.subscribe(
  "mouseClicked",
  function (data) {
    console.log(
      "I am Bob's callback function for a mouse clicked event and this is my event data: " +
        JSON.stringify(data)
    );
  }
);

var subscriptionID2 = publisherSubscriber.subscribe(
  "mouseHovered",
  function (data) {
    console.log(
      "I am Bob's callback function for a hovered mouse event and this is my event data: " +
        JSON.stringify(data)
    );
  }
);

var subscriptionID3 = publisherSubscriber.subscribe(
  "mouseClicked",
  function (data) {
    console.log(
      "I am Alice's callback function for a mouse clicked event and this is my event data: " +
        JSON.stringify(data)
    );
  }
);

// CHÚ Ý: sau khi xuất bản một event với dữ liệu của nó, tất cả
// các callback đã được subscribed sẽ chạy và sẽ nhận được
// đối tượng data từ đối tượng đã fire event
// có 3 console.log được thực thi
publisherSubscriber.publish("mouseClicked", { data: "data1" });
publisherSubscriber.publish("mouseHovered", { data: "data2" });

// chúng ta unsubscribe khỏi một sự kiện bằng cách xóa bỏ subscribtion ID
publisherSubscriber.unsubscribe("mouseClicked", subscriptionID3);

// có 2 console.log được chạy
publisherSubscriber.publish("mouseClicked", { data: "data1" });
publisherSubscriber.publish("mouseHovered", { data: "data2" });
```

Design pattern này hữu ích trong trường hợp chúng ta cần thực hiện nhiều thao tác trên khi một sự kiện được thực thi. Hãy tưởng tượng rằng bạn gặp một trường hợp cần phải chạy nhiều API call đến backend và lại thực hiện các API call khác dựa vào kết quả của lần gọi API trước đó. Bạn sẽ lồng các API call này vào dẫn đến khả năng dính callback hell. Sử dụng publisher/subscriber làm cho code thanh lịch hơn đúng không nào.

Mặt trái của pattern này đó là rất khó để test nhiều thành phần của hệ thống. Không có cách ổn định nào để chúng ta biết chắc rằng phần nào của hệ thống sẽ hoạt động hay là không.

### Mediator Pattern

Chúng ta sẽ tóm tắt một pattern cũng rất hữu ích khi nói đến các hệ thống phân lập. Trong trường hợp hệ thống có nhiều thành phần cần kết nối và phối hợp với nhau, có thể giải pháp tốt đó là mediator.

Một mediator là một đối tượng được sử dụng như điểm trung tâm của kết nối giữa các thành phần hệ thống và xử lý quy trình làm việc của chúng. Cần phải nhấn mạnh rằng nó xử lý quy trình làm việc. Tại sao nó lại quan trọng như vậy?

Bởi vì pattern này tương đồng rất lớn so với publisher/subscriber. Bạn có thể tự hỏi: _Ồ, có 2 pattern đều thực hiện việc liên kết giữa các đối tượng, vậy chúng khác nhau gì?_

Cái khác ở chỗ, mediator xử lý quy trình làm việc trong khi publisher/subsciber sử dụng cái gọi là "fire and forget". Publisher/subscriber đơn giản là một trình tổng hợp sự kiện, nghĩa là mó chỉ lquan tâm đến các sự kiện được thực thi và cho biết những subscriber nào biết các sự kiện đã được thực thi. Trình tổng hợp sự kiện không cần quan tâm khi một sự kiện đã được thực thi, khác với trường hợp của mediator.

Một ví dụ tiêu biểu của mediator là một giao diện wizard (các hệ điều hành hay có các cửa sổ mà bạn click Next để tiến tới bước tiếp theo). Ví dụ bạn có một form đăng ký lớn với nhiều tiến trình. Thông thường, khi có nhiều thông tin được yêu cầu từ người dùng thì good practice là hãy chia nhỏ thành nhiều bước.

Bằng cách này, code trông sẽ sạch hơn (dễ bảo trì) và người dùng thì không choáng ngợp bởi số lượng thông tin được yêu cầu để hoàn thành đăn ký. Một mediator là một đối tượng sẽ giữ chức năng xử lý quy trình đăng ký, tính đến các luồng làm việc khác nhau có thể xảy ra do thực tế mỗi người dùng có thể có một quy trình riêng biệt.

Lợi ích rõ ràng từ design pattern này đó là kết nối các thành phần khác nhau của hệ thống, thông qua mediator và code đẹp hơn.

Nhược điểm của pattern này đó là chúng ta đang đem đến một điểm lỗi vào hệ thống, nghĩa là nếu mediator lỗi, toàn bộ hệ thống có thể không làm việc.

### Prototype pattern

Như chúng ta đã nhắc đến trong suốt bài viết, về bản chất Javascript không hỗ trợ class. Việc thừa kế giữa các đối tượng thông qua prototype.

Nó cho phép chúng ta tạo ra các đối tượng có thể dùng làm prototype cho các đối tượng khác đang được khởi tạo. Đối tượng prototype được dùng như một bản thiết kế (blueprint) cho mỗi đối tượng được construct.

Chúng ta đã nói đến vấn đề này trong phần trước, hãy xem một ví dụ nhỏ để xem pattern này được sử dụng như thế nào.

```javascript
const personPrototype = {
  sayHi: function () {
    console.log("Hello, my name is " + this.name + ", and I am " + this.age);
  },
  sayBye: function () {
    console.log("Bye Bye!");
  },
};

function Person(name, age) {
  name = name || "John Doe";
  age = age || 26;

  function constructorFunction(name, age) {
    this.name = name;
    this.age = age;
  }

  constructorFunction.prototype = personPrototype;

  var instance = new constructorFunction(name, age);
  return instance;
}

var person1 = Person();
var person2 = Person("Bob", 38);

// In ra Hello, my name is John Doe, and I am 26
person1.sayHi();
// In ra Hello, my name is Bob, and I am 38
person2.sayHi();
```

Chú ý cách thừa kế prototype sẽ giúp tăng tốc hệ thống bởi vì cả hai đối tượng tham chiếu đến các hàm được triển khai trong prototype của chúng, thay vì từng đối tượng.

### Command pattern

Command pattern hữu ích trong trường hợp khi bạn muốn phân tách các đối tượng thực thi lệnh khỏi các đối tượng phát lệnh. Ví dụ, hãy tưởng tượng một trường hợp khi ứng dụng của bạn gọi rất nhiều API. Rồi sau đó các API này thay đổi thì bạn phải sửa lại tất cả những chỗ code đã gọi API bị thay đổi.

Đây là nơi cần phải thực hiện một tầng abstraction (trừu tượng) giúp tách các đối tượng đang gọi API ra khỏi các đối tượng ra lệnh gọi. Bằng cách này bạn tránh được việc chỉnh sửa tất cả những nơi đã gọi API và chỉ sửa một chỗ duy nhất.

Cũng như bất kỳ pattern nào khác, chúng ta cần biết chính xác khi nào thì cần một mẫu như vậy. Bạn cần hiểu được những đánh đổi mình đang tạo ra khi thêm một tầng abstraction vào API call sẽ làm giảm hiệu năng của hệ thống nhưng có thể tiết kiệm được rất nhiều thời gian khi ta cần chỉnh sửa các đối tượng thực thi các command.

```javascript
// đối tượng biết khi nào thực thi command
const invoker = {
  add: function (x, y) {
    return x + y;
  },
  subtract: function (x, y) {
    return x - y;
  },
};

// đối tượng được dùng như tầng abstraction
// khi thực thi  các command, nó đại diện cho invoker
const manager = {
  execute: function (name, args) {
    if (name in invoker) {
      return invoker[name].apply(invoker, [].slice.call(arguments, 1));
    }
    return false;
  },
};

// In ra 8
console.log(manager.execute("add", 3, 5));
// In ra 2
console.log(manager.execute("subtract", 5, 3));
```

### Facade pattern

Facade pattern được dùng khi bạn muốn tạo ra một tầng abstraction giữa public và private. Nó được sử dụng khi cần một giao diện đơn giản hơn.

Một ví dụ điển hình đó là các thư viện chỉnh sửa DOM như JQuery, Dojo, D3. Bạn có thể thấy rằng khi sử dụng các thư viện này, chúng có các tính năng select rất mạnh, có thể viết một câu truy vấn phức tạp như sau:

```javascript
jQuery(".parent .child div.span");
```

Nó đơn giản hóa rất nhiều tính năng truy cập DOM, và thậm chí nó còn trông rất ngắn gọn cho toàn bộ một quá trình phức tạp phía sau để thực hiện được điều này.

Chúng ta cũng cần nhận thức được sự cân bằng giữa hiệu suất và tính đơn giản. Nên tránh tạo thêm sự phức tạp nếu nó không đủ có lợi. Trong trường hợp các thư viện nói trên, sự đánh đổi là xứng đáng vì chúng đều là những thư viện rất thành công.

## Tiếp theo

Design pattern là một công cụ vô cùng hữu ích mà bất kỳ một Senior Javascript Developer nào cũng cần phải nhận thức được. Nắm chắc, cụ thể các mẫu thiết kế sẽ vô cùng hữu ích và giúp bạn tiết kiệm được nhiều thời gian trong vòng đời của bất kỳ dự án nào, đặc biệt là phần bảo trì. Việc sửa đổi và duy trì các hệ thống được viết dưới sự trợ giúp của các design pattern phù hợp có một giá trị to lớn.

Để giữ cho bài viết được ngắn gọn, tôi sẽ không nêu thêm ví dụ. Cho những ai quan tâm, cảm hứng to lớn cho bài viết này đến từ các quyển sách : _Design Patterns: Elements of Reusable Object-Oriented Software and Addy Osmani’s Learning JavaScript Design Patterns_. Tôi rất khuyến khích các bạn tìm đọc cả hai quyển.

> Theo Toptal: [The Comprehensive Guide to JavaScript Design Patterns](https://www.toptal.com/javascript/comprehensive-guide-javascript-design-patterns)
