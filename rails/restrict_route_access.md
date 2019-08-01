# Restirct routes

https://guides.rubyonrails.org/routing.html#restricting-the-routes-created

```
class EmployeeOnlyConstraint
  def matches?(request)
    person_id = request.session.dig(:cas_extra_attributes, :person_id)
    return if person_id.blank?

    # only employees are allowed
    Person.find(person_id).try(:employee?)
  end
end

Rails.application.routes.draw do

  constraints(EmployeeOnlyConstraint.new) do  
    namespace :admin do
      resources :airplus_imports
      resources :consolidations
    end
    resources :something_important
  end

  # public
  match "/ready"              => "pages#ready", via: [:get, :post]
  match "/login"              => "sessions#login", via: [:get, :post]
  match "/login_form"         => "sessions#login_form", via: [:get, :post]
  match "/logout"             => "sessions#logout", :as => "logout", via: [:get, :post]
  match "/access_denied"      => "pages#access_denied", via: [:get, :post]
  match "pages/access_denied" => "pages#access_denied", via: [:get, :post]

  # Errors
  get "/404" => "errors#not_found"
  get "/500" => "errors#internal_error"
  get "/502" => "errors#bad_gateway"
  get "/422" => "errors#unprocessable_entity"

  # react search only for logged in
  match "/",      to: "react_searches#index", constraints: EmployeeOnlyConstraint.new, via: :all
  match "/*path", to: "react_searches#index", constraints: EmployeeOnlyConstraint.new, via: :all

  # fallback
  match "/", to: "pages#welcome", via: :all
end

```
