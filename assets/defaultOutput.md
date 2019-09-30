## Default Login Module

**Assembly**
```swift
class LoginAssembly {
    static func assemble() -> UIViewController {
        let view = LoginViewController(nibName: nil, bundle: nil)
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
protocol LoginInteractorProtocol: class {

}

// MARK: View -
protocol LoginViewProtocol: class {

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

    init(interface: LoginViewProtocol,
         interactor: LoginInteractorProtocol,
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

    weak var viewController: UIViewController?
    
    init(view: UIViewController?) {
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
