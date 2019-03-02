

For those who had deal with Android sqlite database before, there must be a times when you had to wrote the schema for each and every models of your app. For once, I tried and it’s just a boring afternoon spent on implementing all the schemas and queries for each models.

Coming from web developer, Django backend has written a well wrapped class for create, read, update and delete(CRUD) any models. Let’s dive in some a few examples of how Django deal with complicated database.

    # models.py
    class SomeModel(models.Model):
         name = models.CharField(max_length=100)
    # views.py
          somemodels = SomeModel.objects.all() # list SomeModel
          randommodel = SomeModel.objects.filter(name="random name") # access some random model 

Easy right?

This is what [documentation about android sqlite database](https://developer.android.com/training/basics/data-storage/databases.html#DbHelper):

    public class FeedReaderDbHelper extends SQLiteOpenHelper {
        // If you change the database schema, you must increment the database version.
        public static final int DATABASE_VERSION = 1;
        public static final String DATABASE_NAME = "FeedReader.db";
    
        public FeedReaderDbHelper(Context context) {
            super(context, DATABASE_NAME, null, DATABASE_VERSION);
        }
        public void onCreate(SQLiteDatabase db) {
            db.execSQL(SQL_CREATE_ENTRIES);
        }
        public void onUpgrade(SQLiteDatabase db, int oldVersion, int newVersion) {
            // This database is only a cache for online data, so its upgrade policy is
            // to simply to discard the data and start over
            db.execSQL(SQL_DELETE_ENTRIES);
            onCreate(db);
        }
        public void onDowngrade(SQLiteDatabase db, int oldVersion, int newVersion) {
            onUpgrade(db, oldVersion, newVersion);
        }
    }

Crap, all these lines and we haven’t even started writing our models class yet. For android starters, this complex database schema is enough to scare half of them away(not scientifically proven). Hence, I started my quest to find a gradle package which is easy to use and readable. It doesn’t take long to stumble upon this [insanely easy to use android database wrapper : SugarORM](http://satyan.github.io/sugar/getting-started.html).

Sugar ORM basically helps you create all the tables, query, update, delete schema for all the models you needed to store in sqlite database. Simply extends SugarRecord and you are done.

    /* Example from github [https://github.com/chennaione/sugar](https://github.com/chennaione/sugar) */
    public class Book extends SugarRecord {
      @Unique
      String isbn;
      String title;
      String edition;
    
      // Default constructor is necessary for SugarRecord
      public Book() {
    
      }
    
      public Book(String isbn, String title, String edition) {
        this.isbn = isbn;
        this.title = title;
        this.edition = edition;
      }
    }
    /* create */
    Book book = new Book("isbn123", "Title here", "2nd edition")
    book.save();
    /*  read */
    Book book = Book.findById(Book.class, 1);
    /* delete */
    SugarRecord.delete(book);
    /* update */
    SugarRecord.update(book);

No complex query schema needed. Sweet right?

Before you jump into the pool of sweet simple codes, there’s a twist.

![[“Official documentation” ](http://satyan.github.io/sugar/getting-started.html)This is not the version you want. You need version 1.4 or above](https://cdn-images-1.medium.com/max/2000/1*6y1jA-XVzRqWZ13CRBNuCA.png)*[“Official documentation” ](http://satyan.github.io/sugar/getting-started.html)This is not the version you want. You need version 1.4 or above*

First, [the official document](http://satyan.github.io/sugar/getting-started.html) was outdated. The tutorial actually point users to use a 1.3 version package while the newest version is 1.5 at this time of writing. During my testing in version 1.3, there’s a manifest merge error occured, which was pointed out by issue #746 and #169. It was this very moment when I found out the “latest” documentation was actually the readme in github repository not the documentation web page. I upgraded to version 1.5 and happily sync my gradle. No errors. Nice.

![Screenshot from SugarORM github. And no, this link is not the official documentation, you are looking the official documentation right now!](https://cdn-images-1.medium.com/max/2100/1*MOOssu5C_4IwIZGFnwNY6w.png)*Screenshot from SugarORM github. And no, this link is not the official documentation, you are looking the official documentation right now!*

Second, no one really tells me I need to change my database version whenever I updated any of my sugar sweet database models. If you don’t do this, you may stumble upon “**no such table exception error**”. Which conveniently, is the **same errors **when you:

1. Didn’t add the proper domain name package meta field in Manifest tag

1. Forgot to add android:name="com.orm.SugarApp"in the Manifest application tag

1. Enable Instant Run features in android studio 2/3.

1. In some case, having a very long db file name.

Crap, that’s a lot to troubleshoot. In my case, I need to disable instant run, change to a shorter db name, add the missing tags in manifest and clear the old database file from my development phone.

## Does all the hard work it worth it? Yes.

Since, there isn’t any troubleshoot page written in the official documentation, I decided to write this in hope anyone who read this would never had to go though all the issues to fix some trivial errors anymore.

## TLDR;

if you plan to use SugarORM in your next project or integrate this to any of your existing project. Here’s some notes you may need to be aware of.

1. Always use the latest version ≥1.5

1. This is the only [documentation](https://github.com/chennaione/sugar) you ever need for SugarORM

1. If you don’t want to change database version every time you made a change to the class member, you will need to do the extra steps to clear the app data manually.

1. Disable instant run and check any improper meta field in AndroidManifest
