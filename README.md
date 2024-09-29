# Library-Management-System
Simple Library Management System
books = []
users = []

class Book:
    def __init__(self,book_id,title,author,genre):
        self.book_id = book_id
        self.title = title
        self.author = author
        self.genre = genre
        self.status = 'available'
    def __str__(self):
        return f"[{self.book_id}] {self.title} by {self.author} (Genre: {self.genre},Status: {self.status})"
class User:
    def __init__(self,user_id,name):
        self.user_id = user_id
        self.name = name
        self.borrowed_books = []
    def __str__(self):
        return f"[{self.user_id}] {self.name}, Borrowed Books: {[book.title for book in self.borrowed_books ]}"
    
def main_menu():
    while True:
        print("\nCommunity Library")
        print("1.Add Books")
        print("2.View Books")
        print("3.Search Books")
        print("4.Add User")
        print("5.Borrow Book")
        print("6.Return Book")
        print("7.Exit")

        choice = input("Choose an option: ")
        if choice == '1':
            add_books()
        elif choice == '2':
            view_books()
        elif choice == '3':
            search_books()
        elif choice == '4':
            add_user()
        elif choice == '5':
            borrow_book()
        elif choice == '6':
            return_book()
        elif choice == '7':
            print("Exiting the system")
            break
        else:
            print("Invalid choice.Please try again.")
def add_books():
    book_id = input("Enter Book Id: ")
    title = input("Enter Book title: ")
    author = input("Enter author name: ")
    genre = input("Enter genre: ")
    new_book = Book(book_id,title,author,genre)
    books.append(new_book)
    print("Book added successfully!")
def view_books():
    if not books:
        print("No books available")
    else:
        for book in books:
            print(book)
def add_user():
    user_id = input("Enter user id: ")
    name = input("Enter user name: ")
    new_user  = User(user_id,name)
    users.append(new_user)
    print("User added successfully!")
def display_users():
    if not users:
        print("No user available!")
    else:
        for user in users:
            print(user)
def borrow_book():
    user_id = input("Enter user id: ")
    book_id = input("Enter book id to borrow book: ")
    user = next((u for u in users if u.user_id == user_id),None)
    book = next((b for b in books if b.book_id == book_id),None)


    
    if user and book:
        if book.status == 'available':
            book.status = 'checked out'
            user.borrowed_books.append(book)
            print(f"{user.name} borrowed '{book.title}'.")
        else:
            print("Book is currently unavailable.")
    else:
        print("Invalid user ID or book ID.")

def return_book():
    user_id = input("Enter user ID: ")
    book_id = input("Enter book ID to return: ")

    user = next((u for u in users if u.user_id == user_id), None)
    book = next((b for b in books if b.book_id == book_id), None)

    if user and book in user.borrowed_books:
        book.status = 'available'
        user.borrowed_books.remove(book)
        print(f"{user.name} returned '{book.title}'.")
    else:
        print("Invalid return request.")
def search_books():
    query = input("Enter title, author, or genre to search: ")
    results = [book for book in books if query.lower() in (book.title.lower() + book.author.lower() + book.genre.lower())]

    if results:
        for book in results:
            print(book)
    else:
        print("No books found.")
def display_books_by_status(status):
    filtered_books = [book for book in books if book.status == status]
    if filtered_books:
        for book in filtered_books:
            print(book)
    else:
        print(f"No books with status '{status}' available.")
def safe_input(prompt, valid_options=None):
    while True:
        user_input = input(prompt).strip()
        if valid_options and user_input not in valid_options:
            print(f"Please enter one of the following options: {', '.join(valid_options)}")
        else:
            return user_input
if __name__ == "__main__":
    main_menu()





        
        
