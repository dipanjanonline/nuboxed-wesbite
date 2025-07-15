import React, { useState, useEffect } from "react";

export default function App() {
  const [activePage, setActivePage] = useState("home");
  const [darkMode, setDarkMode] = useState(false);
  const [mobileMenuOpen, setMobileMenuOpen] = useState(false);
  const [orderModalOpen, setOrderModalOpen] = useState(false);
  const [orderItem, setOrderItem] = useState(null);

  const [formData, setFormData] = useState({
    name: "",
    company: "",
    email: "",
    phone: "",
    item: "",
  });

  // Load dark mode from localStorage
  useEffect(() => {
    const savedMode = localStorage.getItem("darkMode") === "true";
    setDarkMode(savedMode);
    if (savedMode) document.documentElement.classList.add("dark");
  }, []);

  const toggleDarkMode = () => {
    const newMode = !darkMode;
    setDarkMode(newMode);
    if (newMode) {
      document.documentElement.classList.add("dark");
      localStorage.setItem("darkMode", "true");
    } else {
      document.documentElement.classList.remove("dark");
      localStorage.setItem("darkMode", "false");
    }
  };

  const handleInputChange = (e) => {
    const { name, value } = e.target;
    setFormData((prev) => ({ ...prev, [name]: value }));
  };

  const handleSubmit = (e) => {
    e.preventDefault();
    alert(`Thank you, ${formData.name}! Your order for "${formData.item}" has been received.`);
    setOrderModalOpen(false);
  };

  const services = [
    { id: "repairs", name: "Repairs", description: "Precision repairs using OEM parts in state-of-the-art facilities." },
    { id: "testing", name: "Testing", description: "Automated and manual testing for functionality and durability." },
    { id: "certification", name: "Certification", description: "ISO-certified processes to ensure product quality and safety." },
    { id: "trading", name: "Trading", description: "Global trading of refurbished electronics with compliance and traceability." }
  ];

  const products = [
    { id: "circle-erp", name: "Circle ERP", description: "SaaS platform built specifically for reverse logistics automation." },
    { id: "faraday-ai", name: "Faraday.ai Diagnostic Robot", description: "AI-powered robot that tests, grades, and certifies phones automatically." },
    { id: "repair-tools", name: "Repair Tools", description: "Professional-grade tools designed for efficiency and precision." },
    { id: "oem-spares", name: "OEM Spares", description: "Genuine OEM components sourced directly from manufacturers." }
  ];

  const factories = [
    {
      region: "US",
      image: "https://placehold.co/600x400?text=US+Factory",
      capabilities: ["Advanced diagnostics lab", "AI-driven sorting systems", "Eco-friendly recycling units"]
    },
    {
      region: "Europe",
      image: " https://placehold.co/600x400?text=Europe+Factory",
      capabilities: ["ISO 9001 certified", "Automated repair stations", "Zero-landfill policy"]
    },
    {
      region: "UAE",
      image: " https://placehold.co/600x400?text=UAE+Factory",
      capabilities: ["Smart warehouse integration", "High-speed logistics", "Solar-powered operations"]
    },
    {
      region: "India",
      image: " https://placehold.co/600x400?text=India+Factory",
      capabilities: ["Skilled technician workforce", "Cost-effective refurbishment", "Rapid scalability"]
    },
    {
      region: "China",
      image: " https://placehold.co/600x400?text=China+Factory",
      capabilities: ["Mass production lines", "Quality control AI systems", "Integrated supply chain"]
    }
  ];

  const blogPosts = [
    { title: "The Future of Refurbished Electronics", author: "Jane Doe", date: "March 15, 2025" },
    { title: "How Faraday.ai is Revolutionizing Diagnostics", author: "Tech Reviewer", date: "February 28, 2025" },
    { title: "Why Circle ERP is a Game Changer for Reverse Logistics", author: "NuBoxed Team", date: "January 10, 2025" }
  ];

  return (
    <div className="min-h-screen bg-gray-50 text-gray-900 transition-colors duration-300 dark:bg-gray-900 dark:text-white">
      {/* Header */}
      <header className="bg-white shadow-md sticky top-0 z-50 dark:bg-gray-800">
        <div className="container mx-auto px-4 py-4 flex justify-between items-center">
          <h1 className="text-2xl font-bold text-[#f04a27]">Nuboxed</h1>
          <nav className="hidden md:flex space-x-6">
            <button onClick={() => setActivePage("home")} className="hover:text-[#f5803b] transition">Home</button>
            <button onClick={() => setActivePage("services")} className="hover:text-[#f5803b] transition">Services</button>
            <button onClick={() => setActivePage("products")} className="hover:text-[#f5803b] transition">Products</button>
            <button onClick={() => setActivePage("factories")} className="hover:text-[#f5803b] transition">Factories</button>
            <button onClick={() => setActivePage("faraday")} className="hover:text-[#f5803b] transition">Faraday.ai</button>
            <button onClick={() => setActivePage("circle")} className="hover:text-[#f5803b] transition">Circle ERP</button>
            <button onClick={() => setActivePage("blog")} className="hover:text-[#f5803b] transition">Blog</button>
            <button onClick={() => setActivePage("reports")} className="hover:text-[#f5803b] transition">Reports</button>
          </nav>
          <div className="flex items-center space-x-4">
            <button onClick={toggleDarkMode} className="p-2 rounded-full hover:bg-gray-200 dark:hover:bg-gray-700 transition">
              {darkMode ? (
                <svg xmlns="http://www.w3.org/2000/svg" className="h-5 w-5" fill="none" viewBox="0 0 24 24" stroke="currentColor">
                  <path strokeLinecap="round" strokeLinejoin="round" strokeWidth={2} d="M12 3v1m0 16v1m9-9h-1M4 12H3m15.364 6.364l-.707-.707M6.343 6.343l-.707-.707m12.728 0l-.707.707M6.343 17.657l-.707.707M16 12a4 4 0 11-8 0 4 4 0 018 0z" />
                </svg>
              ) : (
                <svg xmlns="http://www.w3.org/2000/svg" className="h-5 w-5" fill="none" viewBox="0 0 24 24" stroke="currentColor">
                  <path strokeLinecap="round" strokeLinejoin="round" strokeWidth={2} d="M20.354 15.354A9 9 0 018.646 3.646 9.003 9.003 0 0012 21a9.003 9.003 0 008.354-5.646z" />
                </svg>
              )}
            </button>
            <button onClick={() => setMobileMenuOpen(true)} className="md:hidden p-2 rounded bg-[#f04a27] text-white hover:bg-[#be342f] transition">☰</button>
          </div>
        </div>

        {/* Mobile Drawer */}
        {mobileMenuOpen && (
          <div className="fixed inset-0 bg-black bg-opacity-50 z-40" onClick={() => setMobileMenuOpen(false)}>
            <div className="bg-white dark:bg-gray-800 h-full w-64 p-6 shadow-lg" onClick={(e) => e.stopPropagation()}>
              <button onClick={() => setMobileMenuOpen(false)} className="absolute top-4 right-4 text-xl">×</button>
              <nav className="mt-12 flex flex-col space-y-4 text-lg">
                <button onClick={() => { setActivePage("home"); setMobileMenuOpen(false); }} className="hover:text-[#f5803b] transition">Home</button>
                <button onClick={() => { setActivePage("services"); setMobileMenuOpen(false); }} className="hover:text-[#f5803b] transition">Services</button>
                <button onClick={() => { setActivePage("products"); setMobileMenuOpen(false); }} className="hover:text-[#f5803b] transition">Products</button>
                <button onClick={() => { setActivePage("factories"); setMobileMenuOpen(false); }} className="hover:text-[#f5803b] transition">Factories</button>
                <button onClick={() => { setActivePage("faraday"); setMobileMenuOpen(false); }} className="hover:text-[#f5803b] transition">Faraday.ai</button>
                <button onClick={() => { setActivePage("circle"); setMobileMenuOpen(false); }} className="hover:text-[#f5803b] transition">Circle ERP</button>
                <button onClick={() => { setActivePage("blog"); setMobileMenuOpen(false); }} className="hover:text-[#f5803b] transition">Blog</button>
                <button onClick={() => { setActivePage("reports"); setMobileMenuOpen(false); }} className="hover:text-[#f5803b] transition">Reports</button>
              </nav>
            </div>
          </div>
        )}
      </header>

      {/* Hero Section */}
      {activePage === "home" && (
        <section className="bg-gradient-to-r from-[#f04a27] to-[#f5803b] text-white py-20">
          <div className="container mx-auto px-6 text-center animate-fadeInDown">
            <h2 className="text-4xl md:text-5xl font-bold mb-6">Powering the Circular Economy</h2>
            <p className="text-lg md:text-xl max-w-3xl mx-auto mb-8">
              NuBoxed leads global innovation in refurbished electronics with cutting-edge technology and sustainable practices.
            </p>
            <button onClick={() => setActivePage("services")} className="bg-white text-[#f04a27] px-6 py-3 rounded-full font-semibold hover:bg-gray-100 transition">
              Explore Our Solutions
            </button>
          </div>
        </section>
      )}

      {/* Service Detail Pages */}
      {services.some(s => s.id === activePage) && (
        <ServiceDetail service={services.find(s => s.id === activePage)} setOrderItem={setOrderItem} setOrderModalOpen={setOrderModalOpen} />
      )}

      {/* Product Detail Pages */}
      {products.some(p => p.id === activePage) && (
        <ProductDetail product={products.find(p => p.id === activePage)} setOrderItem={setOrderItem} setOrderModalOpen={setOrderModalOpen} />
      )}

      {/* Services Page */}
      {activePage === "services" && <ServicesPage services={services} setActivePage={setActivePage} setOrderItem={setOrderItem} setOrderModalOpen={setOrderModalOpen} />}

      {/* Products Page */}
      {activePage === "products" && <ProductsPage products={products} setActivePage={setActivePage} setOrderItem={setOrderItem} setOrderModalOpen={setOrderModalOpen} />}

      {/* Factories Page */}
      {activePage === "factories" && <FactoriesPage factories={factories} />}

      {/* Faraday.ai Page */}
      {activePage === "faraday" && <FaradayPage setOrderItem={setOrderItem} setOrderModalOpen={setOrderModalOpen} />}

      {/* Circle ERP Page */}
      {activePage === "circle" && <CircleERPPage setOrderItem={setOrderItem} setOrderModalOpen={setOrderModalOpen} />}

      {/* Blog Page */}
      {activePage === "blog" && <BlogPage blogPosts={blogPosts} />}

      {/* Reports Page */}
      {activePage === "reports" && <ReportsPage formData={formData} handleInputChange={handleInputChange} handleSubmit={handleSubmit} />}

      {/* Order Modal */}
      {orderModalOpen && (
        <OrderModal
          formData={formData}
          handleInputChange={handleInputChange}
          handleSubmit={handleSubmit}
          orderItem={orderItem}
          setOrderModalOpen={setOrderModalOpen}
        />
      )}

      {/* Footer */}
      <footer className="bg-gray-800 text-white py-10">
        <div className="container mx-auto px-6">
          <div className="flex flex-col md:flex-row justify-between">
            <div className="mb-6 md:mb-0">
              <h3 className="text-xl font-bold mb-2">Nuboxed</h3>
              <p>Empowering the circular economy through innovation.</p>
            </div>
            <div>
              <h4 className="text-lg font-semibold mb-2">Quick Links</h4>
              <ul className="space-y-1">
                <li><button onClick={() => setActivePage("services")} className="hover:underline">Services</button></li>
                <li><button onClick={() => setActivePage("products")} className="hover:underline">Products</button></li>
                <li><button onClick={() => setActivePage("factories")} className="hover:underline">Factories</button></li>
                <li><button onClick={() => setActivePage("blog")} className="hover:underline">Blog</button></li>
                <li><button onClick={() => setActivePage("reports")} className="hover:underline">Reports</button></li>
              </ul>
            </div>
          </div>
          <div className="mt-8 text-center text-gray-400 text-sm">
            © 2025 Nuboxed. All rights reserved.
          </div>
        </div>
      </footer>

      {/* CSS Animations */}
      <style jsx>{`
        @keyframes fadeInDown {
          from { opacity: 0; transform: translateY(-30px); }
          to { opacity: 1; transform: translateY(0); }
        }
        @keyframes fadeInUp {
          from { opacity: 0; transform: translateY(30px); }
          to { opacity: 1; transform: translateY(0); }
        }
        .animate-fadeInDown { animation: fadeInDown 0.8s ease-out forwards; }
        .animate-fadeInUp { animation: fadeInUp 0.8s ease-out forwards; }
      `}</style>
    </div>
  );
}

// Reusable Components

function ServiceDetail({ service, setOrderItem, setOrderModalOpen }) {
  return (
    <section className="py-16 bg-white dark:bg-gray-900">
      <div className="container mx-auto px-6">
        <div className="max-w-4xl mx-auto bg-gray-100 dark:bg-gray-800 p-8 rounded-lg shadow-lg animate-fadeInUp">
          <img src={` https://placehold.co/800x400?text=${encodeURIComponent(service.name)}`} alt={service.name} className="w-full h-auto rounded mb-6" />
          <h2 className="text-3xl font-bold mb-4">{service.name}</h2>
          <p className="mb-6">{service.description}</p>
          <button onClick={() => { setOrderItem(service.name); setOrderModalOpen(true); }} className="bg-[#f04a27] text-white py-2 px-6 rounded hover:bg-[#be342f] transition">
            Order Service
          </button>
        </div>
      </div>
    </section>
  );
}

function ProductDetail({ product, setOrderItem, setOrderModalOpen }) {
  return (
    <section className="py-16 bg-gray-100 dark:bg-gray-800">
      <div className="container mx-auto px-6">
        <div className="max-w-4xl mx-auto bg-white dark:bg-gray-700 p-8 rounded-lg shadow-lg animate-fadeInUp">
          <img src={` https://placehold.co/800x400?text=${encodeURIComponent(product.name)}`} alt={product.name} className="w-full h-auto rounded mb-6" />
          <h2 className="text-3xl font-bold mb-4">{product.name}</h2>
          <p className="mb-6">{product.description}</p>
          <button onClick={() => { setOrderItem(product.name); setOrderModalOpen(true); }} className="bg-[#f04a27] text-white py-2 px-6 rounded hover:bg-[#be342f] transition">
            Order Product
          </button>
        </div>
      </div>
    </section>
  );
}

function ServicesPage({ services, setActivePage, setOrderItem, setOrderModalOpen }) {
  return (
    <section className="py-16 bg-white dark:bg-gray-900">
      <div className="container mx-auto px-6">
        <h2 className="text-3xl font-bold text-center mb-12 animate-fadeInUp">Our Services</h2>
        <div className="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-4 gap-8">
          {services.map((service, idx) => (
            <div key={idx} className="bg-gray-100 dark:bg-gray-800 p-6 rounded-lg shadow hover:shadow-lg transition transform hover:-translate-y-1 animate-fadeInUp" style={{ animationDelay: `${idx * 100}ms` }}>
              <h3 className="text-xl font-semibold mb-3">{service.name}</h3>
              <p>{service.description}</p>
              <button onClick={() => setActivePage(service.id)} className="mt-4 w-full bg-[#f04a27] hover:bg-[#be342f] text-white py-2 rounded transition">
                Learn More
              </button>
              <button onClick={() => { setOrderItem(service.name); setOrderModalOpen(true); }} className="mt-2 w-full bg-gray-200 hover:bg-gray-300 text-gray-800 py-2 rounded transition">
                Order Service
              </button>
            </div>
          ))}
        </div>
      </div>
    </section>
  );
}

function ProductsPage({ products, setActivePage, setOrderItem, setOrderModalOpen }) {
  return (
    <section className="py-16 bg-gray-100 dark:bg-gray-800">
      <div className="container mx-auto px-6">
        <h2 className="text-3xl font-bold text-center mb-12 animate-fadeInUp">Our Products</h2>
        <div className="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-4 gap-8">
          {products.map((product, idx) => (
            <div key={idx} className="bg-white dark:bg-gray-700 p-6 rounded-lg shadow hover:shadow-xl transition transform hover:scale-105 animate-fadeInUp" style={{ animationDelay: `${idx * 100}ms` }}>
              <h3 className="text-xl font-semibold mb-3">{product.name}</h3>
              <p>{product.description}</p>
              <button onClick={() => setActivePage(product.id)} className="mt-4 w-full bg-[#f04a27] hover:bg-[#be342f] text-white py-2 rounded transition">
                Learn More
              </button>
              <button onClick={() => { setOrderItem(product.name); setOrderModalOpen(true); }} className="mt-2 w-full bg-gray-200 hover:bg-gray-300 text-gray-800 py-2 rounded transition">
                Order Product
              </button>
            </div>
          ))}
        </div>
      </div>
    </section>
  );
}

function FactoriesPage({ factories }) {
  return (
    <section className="py-16 bg-white dark:bg-gray-900">
      <div className="container mx-auto px-6">
        <h2 className="text-3xl font-bold text-center mb-12 animate-fadeInUp">Global Factories</h2>
        <div className="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-3 gap-10">
          {factories.map((factory, idx) => (
            <div key={idx} className="bg-gray-100 dark:bg-gray-800 rounded-lg overflow-hidden shadow hover:shadow-xl transition transform hover:-translate-y-1 animate-fadeInUp" style={{ animationDelay: `${idx * 150}ms` }}>
              <img src={factory.image} alt={`${factory.region} Factory`} className="w-full h-48 object-cover" />
              <div className="p-6">
                <h3 className="text-xl font-semibold mb-3">{factory.region}</h3>
                <ul className="list-disc pl-5 space-y-1">
                  {factory.capabilities.map((cap, i) => (
                    <li key={i}>{cap}</li>
                  ))}
                </ul>
              </div>
            </div>
          ))}
        </div>
      </div>
    </section>
  );
}

function FaradayPage({ setOrderItem, setOrderModalOpen }) {
  return (
    <section className="py-16 bg-gray-100 dark:bg-gray-800">
      <div className="container mx-auto px-6">
        <h2 className="text-3xl font-bold text-center mb-12 animate-fadeInUp">Faraday.ai – The Diagnostic Robot</h2>
        <div className="max-w-4xl mx-auto bg-white dark:bg-gray-700 p-8 rounded-lg shadow-lg animate-fadeInUp">
          <img src=" https://placehold.co/800x400?text=Faraday.ai+Robot" alt="Faraday.ai" className="w-full h-auto rounded mb-6" />
          <p className="mb-4">Faraday.ai is our AI-powered diagnostic robot that automates the testing, grading, and certification of smartphones.</p>
          <p className="mb-6">With real-time analytics and cloud integration, Faraday.ai streamlines the refurbishment process and ensures consistent quality across all devices.</p>
          <button onClick={() => { setOrderItem("Faraday.ai Diagnostic Robot"); setOrderModalOpen(true); }} className="bg-[#f04a27] text-white py-2 px-6 rounded hover:bg-[#be342f] transition">
            Order Faraday.ai
          </button>
        </div>
      </div>
    </section>
  );
}

function CircleERPPage({ setOrderItem, setOrderModalOpen }) {
  return (
    <section className="py-16 bg-white dark:bg-gray-900">
      <div className="container mx-auto px-6">
        <h2 className="text-3xl font-bold text-center mb-12 animate-fadeInUp">Circle ERP – Built for Reverse Logistics</h2>
        <div className="max-w-4xl mx-auto bg-gray-100 dark:bg-gray-800 p-8 rounded-lg shadow-lg animate-fadeInUp">
          <img src=" https://placehold.co/800x400?text=Circle+ERP+Diagram" alt="Circle ERP Diagram" className="w-full h-auto rounded mb-6" />
          <p className="mb-4">Circle ERP is a SaaS platform tailored specifically for the reverse logistics industry.</p>
          <p className="mb-6">With integrations for Faraday.ai and smart warehouses, Circle ERP helps businesses scale efficiently while maintaining compliance and transparency.</p>
          <button onClick={() => { setOrderItem("Circle ERP"); setOrderModalOpen(true); }} className="bg-[#f04a27] text-white py-2 px-6 rounded hover:bg-[#be342f] transition">
            Order Circle ERP
          </button>
        </div>
      </div>
    </section>
  );
}

function BlogPage({ blogPosts }) {
  return (
    <section className="py-16 bg-gray-100 dark:bg-gray-800">
      <div className="container mx-auto px-6">
        <h2 className="text-3xl font-bold text-center mb-12 animate-fadeInUp">Blog</h2>
        <div className="grid grid-cols-1 md:grid-cols-3 gap-8">
          {blogPosts.map((post, idx) => (
            <div key={idx} className="bg-white dark:bg-gray-700 p-6 rounded-lg shadow hover:shadow-xl transition animate-fadeInUp" style={{ animationDelay: `${idx * 200}ms` }}>
              <h3 className="text-xl font-semibold mb-2">{post.title}</h3>
              <p className="text-sm text-gray-500 mb-1">By {post.author}</p>
              <p className="text-sm text-gray-500">{post.date}</p>
            </div>
          ))}
        </div>
      </div>
    </section>
  );
}

function ReportsPage({ formData, handleInputChange, handleSubmit }) {
  return (
    <section className="py-16 bg-white dark:bg-gray-900">
      <div className="container mx-auto px-6">
        <h2 className="text-3xl font-bold text-center mb-12 animate-fadeInUp">Download Reports & Whitepapers</h2>
        <div className="max-w-2xl mx-auto bg-gray-100 dark:bg-gray-800 p-8 rounded-lg shadow-lg">
          <form onSubmit={handleSubmit}>
            <input type="hidden" name="item" value={formData.item} />
            <div className="mb-4 animate-fadeInUp" style={{ animationDelay: '100ms' }}>
              <label className="block text-sm font-medium mb-1">Name</label>
              <input type="text" name="name" value={formData.name} onChange={handleInputChange} required className="w-full p-2 border border-gray-300 dark:border-gray-600 rounded" />
            </div>
            <div className="mb-4 animate-fadeInUp" style={{ animationDelay: '200ms' }}>
              <label className="block text-sm font-medium mb-1">Company Name</label>
              <input type="text" name="company" value={formData.company} onChange={handleInputChange} required className="w-full p-2 border border-gray-300 dark:border-gray-600 rounded" />
            </div>
            <div className="mb-4 animate-fadeInUp" style={{ animationDelay: '300ms' }}>
              <label className="block text-sm font-medium mb-1">Email</label>
              <input type="email" name="email" value={formData.email} onChange={handleInputChange} required className="w-full p-2 border border-gray-300 dark:border-gray-600 rounded" />
            </div>
            <div className="mb-6 animate-fadeInUp" style={{ animationDelay: '400ms' }}>
              <label className="block text-sm font-medium mb-1">Phone Number</label>
              <input type="tel" name="phone" value={formData.phone} onChange={handleInputChange} required className="w-full p-2 border border-gray-300 dark:border-gray-600 rounded" />
            </div>
            <button type="submit" className="w-full bg-[#f04a27] text-white py-3 rounded hover:bg-[#be342f] transition animate-fadeInUp" style={{ animationDelay: '500ms' }}>
              Download Reports
            </button>
          </form>
        </div>
      </div>
    </section>
  );
}

function OrderModal({ formData, handleInputChange, handleSubmit, orderItem, setOrderModalOpen }) {
  return (
    <div className="fixed inset-0 z-50 flex items-center justify-center bg-black bg-opacity-50">
      <div className="bg-white dark:bg-gray-800 p-8 rounded-lg shadow-lg w-full max-w-md mx-4">
        <button onClick={() => setOrderModalOpen(false)} className="absolute top-4 right-4 text-xl">×</button>
        <h2 className="text-2xl font-bold mb-4">Order {orderItem}</h2>
        <form onSubmit={handleSubmit}>
          <input type="hidden" name="item" value={orderItem} />
          <div className="mb-4">
            <label className="block text-sm font-medium mb-1">Name</label>
            <input type="text" name="name" value={formData.name} onChange={handleInputChange} required className="w-full p-2 border border-gray-300 dark:border-gray-600 rounded" />
          </div>
          <div className="mb-4">
            <label className="block text-sm font-medium mb-1">Company Name</label>
            <input type="text" name="company" value={formData.company} onChange={handleInputChange} required className="w-full p-2 border border-gray-300 dark:border-gray-600 rounded" />
          </div>
          <div className="mb-4">
            <label className="block text-sm font-medium mb-1">Email</label>
            <input type="email" name="email" value={formData.email} onChange={handleInputChange} required className="w-full p-2 border border-gray-300 dark:border-gray-600 rounded" />
          </div>
          <div className="mb-6">
            <label className="block text-sm font-medium mb-1">Phone Number</label>
            <input type="tel" name="phone" value={formData.phone} onChange={handleInputChange} required className="w-full p-2 border border-gray-300 dark:border-gray-600 rounded" />
          </div>
          <button type="submit" className="w-full bg-[#f04a27] text-white py-3 rounded hover:bg-[#be342f] transition">
            Submit Order
          </button>
        </form>
      </div>
    </div>
  );
}