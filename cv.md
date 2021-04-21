# KsArT
![Profile photo](/images/profile_photo.png)

## Contact Info:
[![ksart.it@gmail.com](/images/email_logo.png)](mailto:ksart.it@gmail.com)
[![LinkedIn](/images/linkedin_logo.png)](https://www.linkedin.com/in/ksart-it/)
[![Facebook](/images/facebook_logo.png)](https://www.facebook.com/ksart.it/)
[![Telegram](/images/telegram_logo.png)](https://t.me/KsArT_IT)

## Summary:
I am a system administrator. I always dreamed of becoming a programmer. I decided to fulfill my dream and become a programmer. I have chosen the direction of developing mobile applications.

## Skills:
* **Languages:** Kotlin, Java, Delphi
* **Architecture patterns:** MVP, MVVM
* **Frameworks:** 
* **Database:** SQL, SQLite, RoomDao
* **VCS:** Git, Github, Gitlab

## Code example:
```kotlin
class AddMediaDialogFragment : BottomSheetDialogFragment() {
    private val viewModel: AddMediaViewModel by viewModels()
    private var _viewBinding: DialogMediaAddBinding? = null
    private val viewBinding: DialogMediaAddBinding get() = _viewBinding!!
    private lateinit var createMediaLauncher: ActivityResultLauncher<String>
    private var urlMedia = ""

    override fun onCreate(savedInstanceState: Bundle?) {
        super.onCreate(savedInstanceState)
        initCreateMediaLauncher()
    }

    override fun onCreateView(inflater: LayoutInflater, container: ViewGroup?, savedInstanceState: Bundle?): View {
        _viewBinding = DialogMediaAddBinding.inflate(LayoutInflater.from(requireContext()))
        return viewBinding.root
    }

    override fun onDestroyView() {
        super.onDestroyView()
        _viewBinding = null
    }

    override fun onViewCreated(view: View, savedInstanceState: Bundle?) {
        super.onViewCreated(view, savedInstanceState)
        initButton()
        bindViewModel()
        initUrl()
    }

    private fun initUrl() {
        viewBinding.nameTextField.editText?.text?.takeIf {
            it.isBlank()
        }?.let {
            viewBinding.nameTextField.editText?.setText(R.string.media_name_1)
        }
        viewBinding.urlTextField.editText?.text?.takeIf {
            it.isBlank()
        }?.let {
            viewBinding.urlTextField.editText?.setText(R.string.media_url_1,)
        }
    }

    private fun initButton() {
        viewBinding.saveButton.setOnClickListener {
            val name = viewBinding.nameTextField.editText?.text?.toString().orEmpty()
            val url = viewBinding.urlTextField.editText?.text?.toString().orEmpty()
            viewModel.saveMedia(name, url)
        }
        viewBinding.saveAsButton.setOnClickListener {
            val name = viewBinding.nameTextField.editText?.text?.toString().orEmpty()
            urlMedia = viewBinding.urlTextField.editText?.text?.toString().orEmpty()
            createFile(name)
        }
    }

    private fun bindViewModel() {
        viewModel.isLoading.observe(viewLifecycleOwner, ::setLoading)
        viewModel.isToast.observe(viewLifecycleOwner, ::toast)
        viewModel.isSaveSuccess.observe(viewLifecycleOwner) { dismiss() }
    }

    private fun initCreateMediaLauncher() {
        createMediaLauncher = registerForActivityResult(
            ActivityResultContracts.CreateDocument()
        ) { uri ->
            handleCreateFile(uri)
        }
    }

    private fun handleCreateFile(uri: Uri?) {
        if (uri == null) {
            toast("file not created")
            return
        }
        viewModel.saveAsMedia(uri, urlMedia)
    }

    private fun createFile(name: String) {
        createMediaLauncher.launch(name)
    }

    private fun setLoading(isLoading: Boolean) {
        viewBinding.progressBar.isVisible = isLoading
        viewBinding.contentGroup.isVisible = isLoading.not()
    }
}
```

## Experience:
### -


## Education:
* **Java - JavaRush.ru** 2019 - 2020

* **Android Academy Global** 2020

## Languages:
* **English (A1)**
* **Russian**
* **Ukranian**
