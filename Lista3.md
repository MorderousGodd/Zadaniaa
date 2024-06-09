book.py

class Book:
    def __init__(self, title, author, year):
        self.title = title
        self.author = author
        self.year = year

    def __repr__(self):
        return f"{self.title} by {self.author}, {self.year}"


library.py

from book import Book


def _merge(left, right, key):
    result = []
    while left and right:
        if getattr(left[0], key) <= getattr(right[0], key):
            result.append(left.pop(0))
        else:
            result.append(right.pop(0))
    result.extend(left or right)
    return result


class Library:
    def __init__(self):
        self.books = []

    def add_book(self, title, author, year):
        new_book = Book(title, author, year)
        self.books.append(new_book)
        print(f"Added book: {new_book}")

    def remove_book(self, title):
        for book in self.books:
            if book.title == title:
                self.books.remove(book)
                print(f"Removed book: {book}")
                return
        print("Book not found")

    def search_books(self, title=None, author=None, year=None):
        results = [book for book in self.books if
                   (title is None or book.title == title) and
                   (author is None or book.author == author) and
                   (year is None or book.year == year)]
        return results

    def sort_books(self, key, algorithm="quicksort"):
        if key not in {"title", "author", "year"}:
            raise ValueError("Invalid sort key")
        if algorithm == "quicksort":
            self.books = self._quicksort(self.books, key)
        elif algorithm == "mergesort":
            self.books = self._mergesort(self.books, key)
        else:
            raise ValueError("Invalid sort algorithm")

    def _quicksort(self, books, key):
        if len(books) <= 1:
            return books
        pivot = getattr(books[len(books) // 2], key)
        left = [book for book in books if getattr(book, key) < pivot]
        middle = [book for book in books if getattr(book, key) == pivot]
        right = [book for book in books if getattr(book, key) > pivot]
        return self._quicksort(left, key) + middle + self._quicksort(right, key)

    def _mergesort(self, books, key):
        if len(books) <= 1:
            return books
        middle = len(books) // 2
        left = self._mergesort(books[:middle], key)
        right = self._mergesort(books[middle:], key)
        return _merge(left, right, key)

    def display_books(self):
        for book in self.books:
            print(book)


main.py

from library import Library


def main():
    library = Library()
    while True:
        print("\nLibrary Menu:")
        print("1. Add book")
        print("2. Remove book")
        print("3. Search books")
        print("4. Sort books")
        print("5. Display books")
        print("6. Exit")
        choice = input("Enter your choice: ")

        if choice == "1":
            title = input("Enter title: ")
            author = input("Enter author: ")
            year = input("Enter year: ")
            library.add_book(title, author, year)
        elif choice == "2":
            title = input("Enter title of the book to remove: ")
            library.remove_book(title)
        elif choice == "3":
            title = input("Enter title (or leave blank): ") or None
            author = input("Enter author (or leave blank): ") or None
            year = input("Enter year (or leave blank): ") or None
            results = library.search_books(title, author, year)
            if results:
                print("Search results:")
                for book in results:
                    print(book)
            else:
                print("No books found")
        elif choice == "4":
            key = input("Enter sort key (title, author, year): ")
            algorithm = input("Enter sort algorithm (quicksort, mergesort): ")
            library.sort_books(key, algorithm)
        elif choice == "5":
            library.display_books()
        elif choice == "6":
            break
        else:
            print("Invalid choice, please try again.")


if __name__ == "__main__":
    main()
