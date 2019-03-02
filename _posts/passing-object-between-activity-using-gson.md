
# Passing Object between Android Activity using Gson

So you wanna pass data between different activity however you are passing a custom object list which is not parseable using putExtra function.

Hence your options include : Parcelable, Serializable, Gson+Type token. For performance wise, Parcelable is noticeable faster then the later two. However, for code maintainability, Gson is much better than both thanks to less additional method code and the flexibility for list object parsing.

In this section I will talk about how to use gson with type token to pass custom object list through intent.

Below is an example object which we will be passing. Note annotations are added to each private data.

    import com.google.gson.annotations.SerializedName;

    public class Student{
        @SerializedName("student")
        private String student;

        @SerializedName("id")
        private int studentID;

        public Student(String student, int studentID){
             this.student = student;
             this.studentID = studentID;
        }
    }

When passing data to intent, you need to first initialize a gson object and type for converting the your own object to json string.

    List <Student> students; // this is the data you want to pass

    *Gson *gson = new Gson();
    *Type *type = new *TypeToken*<*List*<Student>>() {}.getType();
    *String *json = gson.toJson(student*s*, type);

    Intent intent = new Intent(getBaseContext(), *YourActivity*.class);

    intent.putExtra(YourNext*Activity*.***ADDITIONAL_STUDENTS***, json);
    

In the onCreate method of the target activity, a similar method was used to deserialize your object from string to object class.

    *Gson *gson = new Gson();
    *String *stringLocation = data.getStringExtra(***ADDITIONAL_LOCATION_EXTRA***);
    if(stringLocation != null) {
        *Type *type = new *TypeToken*<*List*<*com.nctu.bikeline.Model.Location*>>() {
        }.getType();
        objectLocations = gson.fromJson(stringLocation, type);
        *Log*.d("Location Count", *Integer*.toString(objectLocations.size()));
    }
    else{
        *Log*.d("Location Count","failed");
    }

The following method can be considered as serialisation, however in performance wise, it’s slightly faster than usual Serialization method.

![Photo & Data source : [http://blog.prolificinteractive.com/2014/07/18/why-we-love-parcelable/](http://blog.prolificinteractive.com/2014/07/18/why-we-love-parcelable/)](https://cdn-images-1.medium.com/max/2000/1*GpBWHjlp6A3VViEI4g_INg.png)*Photo & Data source : [http://blog.prolificinteractive.com/2014/07/18/why-we-love-parcelable/](http://blog.prolificinteractive.com/2014/07/18/why-we-love-parcelable/)*

In the next article I will be trying using parcelable in my recent project and compare whether there is noticeable improvement between two passing method. Meanwhile be sure to follow me, I will share my thoughts and boring coding stories each week.
