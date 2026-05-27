# cafe-menu-card-
React MenuCard component with cozy design.Props : imageUrl, name, price.Built in Emergent.
import { useState } from 'react'

const menuItems = [
  { id: 1, name: 'Cappuccino', price: 120, category: 'Coffee', img: 'https://images.unsplash.com/photo-1514432324607-a09d9b4aefdd?w=150' },
  { id: 2, name: 'Latte', price: 140, category: 'Coffee', img: 'https://images.unsplash.com/photo-1561047029-3000c68339ca?w=150' },
  { id: 3, name: 'Cold Coffee', price: 100, category: 'Cold', img: 'https://images.unsplash.com/photo-1461023058943-07fcbe16d735?w=150' },
  { id: 4, name: 'Veg Sandwich', price: 80, category: 'Snacks', img: 'https://images.unsplash.com/photo-1528735602780-2552fd46c7af?w=150' },
]

const categories = ['All', 'Coffee', 'Cold', 'Snacks']

export default function MenuCard() {
  const [selected, setSelected] = useState('All')
  const [cart, setCart] = useState([])

  const filtered = selected === 'All' 
    ? menuItems 
    : menuItems.filter(item => item.category === selected)

  const addToCart = (item) => {
    setCart([...cart, item])
  }

  return (
    <div className="p-6 bg-gray-50 min-h-screen">
      <h1 className="text-3xl font-bold text-center mb-6 text-amber-800">Cafe Menu Card</h1>
      
      <div className="flex gap-2 justify-center mb-6 flex-wrap">
        {categories.map(cat => (
          <button 
            key={cat}
            onClick={() => setSelected(cat)}
            className={`px-4 py-2 rounded-lg font-medium ${selected === cat ? 'bg-amber-600 text-white' : 'bg-white text-gray-700 border'}`}
          >
            {cat}
          </button>
        ))}
      </div>

      <div className="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-3 gap-4 mb-8">
        {filtered.map(item => (
          <div key={item.id} className="bg-white p-4 rounded-lg shadow-md">
            <img src={item.img} alt={item.name} className="w-full h-40 object-cover rounded mb-3" />
            <h3 className="font-bold text-lg">{item.name}</h3>
            <p className="text-gray-600 mb-3">₹{item.price}</p>
            <button 
              onClick={() => addToCart(item)}
              className="w-full bg-amber-600 hover:bg-amber-700 text-white px-3 py-2 rounded font-medium"
            >
              Add to Cart
            </button>
          </div>
        ))}
      </div>

      <div className="bg-white p-4 rounded-lg shadow-md max-w-md mx-auto">
        <h2 className="font-bold text-xl mb-3">Cart: {cart.length} items</h2>
        <p className="font-bold text-lg">Total: ₹{cart.reduce((sum, item) => sum + item.price, 0)}</p>
      </div>
    </div>
  
}
