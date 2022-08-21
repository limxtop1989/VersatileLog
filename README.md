# VersatileLog
A log library which is time-saving but provides more powerful functions for log, which output the package name, class name and method name where the log statement is invoked automatically. The saved time will be significient when abundant logs needed.

# Download
Gradle:
```
implementation 'io.github.limxtop1989:versatile-log:1.0.1'
```

or Maven:
```
<dependency>
  <groupId>io.github.limxtop1989</groupId>
  <artifactId>versatile-log</artifactId>
  <version>1.0.1</version>
  <type>aar</type>
</dependency>
```
# Usage
1. Initialize versatile log library first in your `Application`.
```
    override fun onCreate() {
        super.onCreate()
        VLog.init(this)
    }
```
2. Developers invoke the API as this below, without providing TAG and message parameter as before.
```kotlin
    override fun onCreateView(
        inflater: LayoutInflater, container: ViewGroup?,
        savedInstanceState: Bundle?
    ): View? {
        VLog.d()// Log a message.
        _binding = FragmentFirstBinding.inflate(inflater, container, false)
        return binding.root
    }
```
Then the VersatileLog output the corresponding log for you as below. The log information contains project name as tag, prefix the class name to the method name where the `VLog.d()` was invoked.
```
96441:08-13 10:25:00.351 20551 20551 D VersatileLog: FirstFragment_onCreateView
```
Developer can watch the output log from terminal by running command providing the project name, class name or the method name or whatever specific log messages.
```
adb logcat -b all | egrep -in --color 'VersatileLog:'
```
3. Provide a specific message if there are multiple log statements in the same method.
```
    override fun onViewCreated(view: View, savedInstanceState: Bundle?) {
        super.onViewCreated(view, savedInstanceState)

        binding.buttonSecond.setOnClickListener {
            VLog.d("start")
            findNavController().navigate(R.id.action_SecondFragment_to_FirstFragment)
            VLog.d("end")
        }
    }
```
4. To watch the value of variable, provide the variable names and values.
```
    fun onAdd(name: String, age: Int) {
        VLog.d(arrayOf("name", "age"), arrayOf(name, age))
    }
```
```
31335:08-13 11:18:50.280  3112  3112 D VersatileLog: SecondFragment_onAdd { name=kitty, age=12 }
```
# Feature
1. Contains package, class and method name automatically for developer in log output.
2. The log function is enable by default in debug version regardless of the log levels.
3. The log function is enable above `INFO` level including in release version, however, developers can enable debug log at runtime without modifing the codes. 


