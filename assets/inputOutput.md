## Login Module with divided Interactor (Input & Output)

**Assembly**
```swift
class LoginAssembly {
    static func assemble() -> UIViewController {
        let view = LoginViewController()
        let interactor = LoginInteractor()
        let router = LoginRouter(view: view)
        let presenter = LoginPresenter(interface: view, interactor: interactor, router: router)

        view.presenter = presenter
        interactor.presenter = presenter

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

}

// MARK: Interactor -
protocol LoginInteractorOutputProtocol: class {

    /* Interactor -> Presenter */
}

protocol LoginInteractorInputProtocol: class {

    /* Presenter -> Interactor */
}

// MARK: View -
protocol LoginViewProtocol: class {

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
    private let interactor: LoginInteractorInputProtocol
    private let router: LoginRouterProtocol

    init(interface: LoginViewProtocol,
         interactor: LoginInteractorInputProtocol,
         router: LoginRouterProtocol) {
        self.view = interface
        self.interactor = interactor
        self.router = router
    }
}
```

**Router**
```swift
class LoginRouter: LoginRouterProtocol {

    weak private var viewController: UIViewController?
    
    init(view: UIViewController) {
        self.viewController = view
    }
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
