## Login Module with divided Interactor (Input & Output)

**Assembly**
```swift
class LoginAssembly {
    static func assemble() -> UIViewController {
        let view = LoginViewController(nibName: nil, bundle: nil)
        let interactor = LoginInteractor()
        let router = LoginRouter()
        let presenter = LoginPresenter(interface: view, interactor: interactor, router: router)

        view.presenter = presenter
        interactor.presenter = presenter
        router.viewController = view

        return view
    }
}

```

**Protocols**
```swift
// MARK: Router -
protocol LoginRouterProtocol: class {

}
// MARK: Presenter -
protocol LoginPresenterProtocol: class {

    var interactor: LoginInteractorInputProtocol? { get set }
}

// MARK: Interactor -
protocol LoginInteractorOutputProtocol: class {

    /* Interactor -> Presenter */
}

protocol LoginInteractorInputProtocol: class {

    var presenter: LoginInteractorOutputProtocol? { get set }

    /* Presenter -> Interactor */
}

// MARK: View -
protocol LoginViewProtocol: class {

    var presenter: LoginPresenterProtocol? { get set }

    /* Presenter -> ViewController */
}
```

**Interactor**
```swift
class LoginInteractor: LoginInteractorInputProtocol {

    weak var presenter: LoginInteractorOutputProtocol?
}
```

**Presenter**
```swift
class LoginPresenter: LoginPresenterProtocol, LoginInteractorOutputProtocol {

    weak private var view: LoginViewProtocol?
    var interactor: LoginInteractorInputProtocol?
    private let router: LoginRouterProtocol

    init(interface: LoginViewProtocol, interactor: LoginInteractorInputProtocol?, router: LoginRouterProtocol) {
        self.view = interface
        self.interactor = interactor
        self.router = router
    }
}
```

**Router**
```swift
class LoginRouter: LoginRouterProtocol {

    weak var viewController: UIViewController?
}

```

**View**
```swift
class LoginViewController: UIViewController, LoginViewProtocol {

    var presenter: LoginPresenterProtocol?

    override func viewDidLoad() {
        super.viewDidLoad()
    }
}
```
