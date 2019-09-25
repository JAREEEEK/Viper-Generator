## Default Login Module

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

}

// MARK: Interactor -
protocol LoginInteractorProtocol: class {

    var presenter: LoginPresenterProtocol? { get set }
}

// MARK: View -
protocol LoginViewProtocol: class {

    var presenter: LoginPresenterProtocol? { get set }
}
```

**Interactor**
```swift
class LoginInteractor: LoginInteractorProtocol {

    weak var presenter: LoginPresenterProtocol?
}
```

**Presenter**
```swift
class LoginPresenter: LoginPresenterProtocol {

    weak private var view: LoginViewProtocol?
    private let interactor: LoginInteractorProtocol
    private let router: LoginRouterProtocol

    init(interface: LoginViewProtocol, interactor: LoginInteractorProtocol, router: LoginRouterProtocol) {
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

    static func createModule() -> UIViewController {

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

**View**
```swift
class LoginViewController: UIViewController, LoginViewProtocol {

    var presenter: LoginPresenterProtocol?

    override func viewDidLoad() {
    super.viewDidLoad()
    }
}
```
