import React, { useState } from 'react';
import { Calendar, Phone, MapPin, Clock, User, Scissors, Star, Menu, X } from 'lucide-react';

const App = () => {
  const [activeTab, setActiveTab] = useState('home');
  const [selectedService, setSelectedService] = useState('');
  const [bookingForm, setBookingForm] = useState({
    name: '',
    phone: '',
    service: '',
    date: '',
    time: ''
  });
  const [mobileMenuOpen, setMobileMenuOpen] = useState(false);

  const services = [
    { name: 'Barbing Sweet Cuts', price: '₦2,000', duration: '30 min', featured: true },
    { name: 'Hair Tint', price: '₦7,500', duration: '45 min', featured: true },
    { name: 'Hair Treatment', price: '₦15,000', duration: '60 min', featured: false },
    { name: 'Hair Dye', price: '₦7,000', duration: '90 min', featured: true },
    { name: 'Hair Growth Services', price: '₦25,000', duration: '2 month', featured: false },
    { name: 'Hair Fixing (Females)', price: '₦3,000', duration: '45 min', featured: true },
    { name: 'Hair Washing (Male & Female)', price: '₦1,500', duration: '20 min', featured: false },
    { name: 'Barber Training', price: 'Contact Us', duration: 'Variable', featured: false }
  ];

  const timeSlots = [
    '9:00 AM', '10:00 AM', '11:00 AM', '12:00 PM',
    '1:00 PM', '2:00 PM', '3:00 PM', '4:00 PM', '5:00 PM'
  ];

  const handleBookingSubmit = (e) => {
    e.preventDefault();
    const whatsappMessage = `Hello P-Moniz Barbing Shop! I'd like to book an appointment:
Name: ${bookingForm.name}
Service: ${bookingForm.service}
Date: ${bookingForm.date}
Time: ${bookingForm.time}
Phone: ${bookingForm.phone}`;
    
    const whatsappUrl = `https://wa.me/2347064427447?text=${encodeURIComponent(whatsappMessage)}`;
    window.open(whatsappUrl, '_blank');
  };

  const NavButton = ({ id, label, icon: Icon }) => (
    <button
      onClick={() => {
        setActiveTab(id);
        setMobileMenuOpen(false);
      }}
      className={`flex items-center space-x-2 px-4 py-2 rounded-lg transition-all ${
        activeTab === id 
          ? 'bg-yellow-400 text-black font-semibold' 
          : 'text-white hover:bg-white/10'
      }`}
    >
      <Icon size={18} />
      <span>{label}</span>
    </button>
  );

  return (
    <div className="min-h-screen bg-gradient-to-br from-gray-900 via-black to-gray-800">
      {/* Header */}
      <header className="bg-black/50 backdrop-blur-md border-b border-yellow-400/20 sticky top-0 z-50">
        <div className="max-w-6xl mx-auto px-4 py-4">
          <div className="flex items-center justify-between">
            <div className="flex items-center space-x-3">
              <div className="w-12 h-12 bg-gradient-to-r from-yellow-400 to-yellow-600 rounded-full flex items-center justify-center">
                <Scissors className="text-black" size={24} />
              </div>
              <div>
                <h1 className="text-2xl font-bold text-white">P-MONIZ</h1>
                <p className="text-yellow-400 text-sm">BARBING SHOP</p>
              </div>
            </div>
            
            {/* Desktop Navigation */}
            <nav className="hidden md:flex space-x-2">
              <NavButton id="home" label="Home" icon={User} />
              <NavButton id="services" label="Services" icon={Scissors} />
              <NavButton id="booking" label="Book Now" icon={Calendar} />
              <NavButton id="contact" label="Contact" icon={Phone} />
            </nav>

            {/* Mobile Menu Button */}
            <button
              onClick={() => setMobileMenuOpen(!mobileMenuOpen)}
              className="md:hidden text-white p-2"
            >
              {mobileMenuOpen ? <X size={24} /> : <Menu size={24} />}
            </button>
          </div>

          {/* Mobile Navigation */}
          {mobileMenuOpen && (
            <nav className="md:hidden mt-4 space-y-2 border-t border-yellow-400/20 pt-4">
              <NavButton id="home" label="Home" icon={User} />
              <NavButton id="services" label="Services" icon={Scissors} />
              <NavButton id="booking" label="Book Now" icon={Calendar} />
              <NavButton id="contact" label="Contact" icon={Phone} />
            </nav>
          )}
        </div>
      </header>

      {/* Main Content */}
      <main className="max-w-6xl mx-auto px-4 py-8">
        {/* Home Tab */}
        {activeTab === 'home' && (
          <div className="space-y-12">
            {/* Hero Section */}
            <section className="text-center space-y-6">
              <div className="inline-flex items-center space-x-2 bg-yellow-400/10 border border-yellow-400/30 rounded-full px-6 py-2">
                <Star className="text-yellow-400" size={20} />
                <span className="text-yellow-400 font-semibold">PREMIUM TOUCH</span>
              </div>
              <h2 className="text-5xl md:text-7xl font-bold text-white leading-tight">
                BARBING<br />
                <span className="text-yellow-400">that Suites your</span><br />
                STYLE
              </h2>
              <p className="text-gray-300 text-lg max-w-2xl mx-auto">
                Experience professional grooming services with our premium touch. 
                From classic cuts to modern styles, we've got you covered.
              </p>
              <button
                onClick={() => setActiveTab('booking')}
                className="bg-gradient-to-r from-yellow-400 to-yellow-600 text-black px-8 py-4 rounded-full font-semibold text-lg hover:shadow-xl hover:shadow-yellow-400/25 transition-all transform hover:scale-105"
              >
                Book Appointment
              </button>
            </section>

            {/* Featured Services */}
            <section className="space-y-8">
              <h3 className="text-3xl font-bold text-white text-center">Popular Services</h3>
              <div className="grid md:grid-cols-3 gap-6">
                {services.filter(service => service.featured).map((service, index) => (
                  <div key={index} className="bg-gradient-to-br from-gray-800 to-gray-900 rounded-xl p-6 border border-yellow-400/20 hover:border-yellow-400/40 transition-all">
                    <div className="flex items-center justify-between mb-4">
                      <Scissors className="text-yellow-400" size={24} />
                      <span className="text-yellow-400 font-bold text-lg">{service.price}</span>
                    </div>
                    <h4 className="text-white font-semibold text-lg mb-2">{service.name}</h4>
                    <p className="text-gray-400 text-sm">{service.duration}</p>
                  </div>
                ))}
              </div>
            </section>
          </div>
        )}

        {/* Services Tab */}
        {activeTab === 'services' && (
          <div className="space-y-8">
            <div className="text-center space-y-4">
              <h2 className="text-4xl font-bold text-white">Our Services</h2>
              <p className="text-gray-300 text-lg">Professional grooming services tailored to your needs</p>
            </div>
            
            <div className="grid md:grid-cols-2 lg:grid-cols-3 gap-6">
              {services.map((service, index) => (
                <div key={index} className="bg-gradient-to-br from-gray-800 to-gray-900 rounded-xl p-6 border border-gray-700 hover:border-yellow-400/40 transition-all group">
                  <div className="flex items-center justify-between mb-4">
                    <Scissors className="text-yellow-400 group-hover:scale-110 transition-transform" size={24} />
                    <span className="text-yellow-400 font-bold text-lg">{service.price}</span>
                  </div>
                  <h4 className="text-white font-semibold text-lg mb-2">{service.name}</h4>
                  <div className="flex items-center justify-between text-sm">
                    <span className="text-gray-400">Duration: {service.duration}</span>
                    {service.featured && (
                      <span className="bg-yellow-400/20 text-yellow-400 px-2 py-1 rounded text-xs">Popular</span>
                    )}
                  </div>
                </div>
              ))}
            </div>

            <div className="bg-gradient-to-r from-yellow-400/10 to-yellow-600/10 border border-yellow-400/30 rounded-xl p-6 text-center">
              <h3 className="text-white font-semibold text-lg mb-2">Additional Services</h3>
              <p className="text-gray-300 mb-4">We also offer barbing accessories sales and snooker for leisure</p>
              <button
                onClick={() => setActiveTab('contact')}
                className="bg-yellow-400 text-black px-6 py-2 rounded-lg font-semibold hover:bg-yellow-500 transition-colors"
              >
                Contact for Details
              </button>
            </div>
          </div>
        )}

        {/* Booking Tab */}
        {activeTab === 'booking' && (
          <div className="max-w-2xl mx-auto space-y-8">
            <div className="text-center space-y-4">
              <h2 className="text-4xl font-bold text-white">Book Your Appointment</h2>
              <p className="text-gray-300">Choose your service and preferred time</p>
            </div>

            <div className="bg-gradient-to-br from-gray-800 to-gray-900 rounded-xl p-8 border border-yellow-400/20 space-y-6">
              <div className="grid md:grid-cols-2 gap-6">
                <div>
                  <label className="block text-white font-semibold mb-2">Full Name</label>
                  <input
                    type="text"
                    required
                    value={bookingForm.name}
                    onChange={(e) => setBookingForm({...bookingForm, name: e.target.value})}
                    className="w-full bg-gray-700 text-white rounded-lg px-4 py-3 border border-gray-600 focus:border-yellow-400 focus:outline-none transition-colors"
                    placeholder="Enter your full name"
                  />
                </div>
                <div>
                  <label className="block text-white font-semibold mb-2">Phone Number</label>
                  <input
                    type="tel"
                    required
                    value={bookingForm.phone}
                    onChange={(e) => setBookingForm({...bookingForm, phone: e.target.value})}
                    className="w-full bg-gray-700 text-white rounded-lg px-4 py-3 border border-gray-600 focus:border-yellow-400 focus:outline-none transition-colors"
                    placeholder="Your phone number"
                  />
                </div>
              </div>

              <div>
                <label className="block text-white font-semibold mb-2">Select Service</label>
                <select
                  required
                  value={bookingForm.service}
                  onChange={(e) => setBookingForm({...bookingForm, service: e.target.value})}
                  className="w-full bg-gray-700 text-white rounded-lg px-4 py-3 border border-gray-600 focus:border-yellow-400 focus:outline-none transition-colors"
                >
                  <option value="">Choose a service</option>
                  {services.map((service, index) => (
                    <option key={index} value={service.name}>
                      {service.name} - {service.price}
                    </option>
                  ))}
                </select>
              </div>

              <div className="grid md:grid-cols-2 gap-6">
                <div>
                  <label className="block text-white font-semibold mb-2">Preferred Date</label>
                  <input
                    type="date"
                    required
                    value={bookingForm.date}
                    onChange={(e) => setBookingForm({...bookingForm, date: e.target.value})}
                    min={new Date().toISOString().split('T')[0]}
                    className="w-full bg-gray-700 text-white rounded-lg px-4 py-3 border border-gray-600 focus:border-yellow-400 focus:outline-none transition-colors"
                  />
                </div>
                <div>
                  <label className="block text-white font-semibold mb-2">Preferred Time</label>
                  <select
                    required
                    value={bookingForm.time}
                    onChange={(e) => setBookingForm({...bookingForm, time: e.target.value})}
                    className="w-full bg-gray-700 text-white rounded-lg px-4 py-3 border border-gray-600 focus:border-yellow-400 focus:outline-none transition-colors"
                  >
                    <option value="">Select time</option>
                    {timeSlots.map((time, index) => (
                      <option key={index} value={time}>{time}</option>
                    ))}
                  </select>
                </div>
              </div>

              <button
                onClick={handleBookingSubmit}
                className="w-full bg-gradient-to-r from-yellow-400 to-yellow-600 text-black py-4 rounded-lg font-semibold text-lg hover:shadow-xl hover:shadow-yellow-400/25 transition-all transform hover:scale-105"
              >
                Book via WhatsApp
              </button>
            </div>
          </div>
        )}

        {/* Contact Tab */}
        {activeTab === 'contact' && (
          <div className="space-y-8">
            <div className="text-center space-y-4">
              <h2 className="text-4xl font-bold text-white">Get In Touch</h2>
              <p className="text-gray-300">Visit us or reach out for appointments</p>
            </div>

            <div className="grid md:grid-cols-2 gap-8">
              <div className="bg-gradient-to-br from-gray-800 to-gray-900 rounded-xl p-8 border border-yellow-400/20 space-y-6">
                <h3 className="text-2xl font-bold text-white mb-6">Contact Information</h3>
                
                <div className="space-y-4">
                  <div className="flex items-center space-x-4">
                    <div className="w-12 h-12 bg-yellow-400/20 rounded-lg flex items-center justify-center">
                      <MapPin className="text-yellow-400" size={20} />
                    </div>
                    <div>
                      <h4 className="text-white font-semibold">Address</h4>
                      <p className="text-gray-300">8 Oboro Road, Mosqueroad, Amassoma, Bayelsa State</p>
                    </div>
                  </div>

                  <div className="flex items-center space-x-4">
                    <div className="w-12 h-12 bg-yellow-400/20 rounded-lg flex items-center justify-center">
                      <Phone className="text-yellow-400" size={20} />
                    </div>
                    <div>
                      <h4 className="text-white font-semibold">Phone</h4>
                      <p className="text-gray-300">07064427447</p>
                    </div>
                  </div>

                  <div className="flex items-center space-x-4">
                    <div className="w-12 h-12 bg-yellow-400/20 rounded-lg flex items-center justify-center">
                      <Clock className="text-yellow-400" size={20} />
                    </div>
                    <div>
                      <h4 className="text-white font-semibold">Hours</h4>
                      <p className="text-gray-300">Mon - Sat: 9:00 AM - 6:00 PM</p>
                      <p className="text-gray-300">Sunday: Closed</p>
                    </div>
                  </div>

                  <div className="flex items-center space-x-4">
                    <div className="w-12 h-12 bg-yellow-400/20 rounded-lg flex items-center justify-center">
                      <User className="text-yellow-400" size={20} />
                    </div>
                    <div>
                      <h4 className="text-white font-semibold">Instagram</h4>
                      <p className="text-gray-300">@pmonizbabingshop</p>
                    </div>
                  </div>
                </div>

                <div className="flex space-x-4 pt-4">
                  <a
                    href="tel:07064427447"
                    className="flex-1 bg-yellow-400 text-black py-3 rounded-lg font-semibold text-center hover:bg-yellow-500 transition-colors"
                  >
                    Call Now
                  </a>
                  <a
                    href="https://wa.me/2347064427447"
                    target="_blank"
                    rel="noopener noreferrer"
                    className="flex-1 bg-green-600 text-white py-3 rounded-lg font-semibold text-center hover:bg-green-700 transition-colors"
                  >
                    WhatsApp
                  </a>
                </div>
              </div>

              <div className="bg-gradient-to-br from-gray-800 to-gray-900 rounded-xl p-8 border border-yellow-400/20">
                <h3 className="text-2xl font-bold text-white mb-6">Why Choose P-Moniz?</h3>
                <div className="space-y-4">
                  <div className="flex items-start space-x-3">
                    <div className="w-6 h-6 bg-yellow-400 rounded-full flex items-center justify-center mt-1">
                      <span className="text-black text-sm font-bold">✓</span>
                    </div>
                    <div>
                      <h4 className="text-white font-semibold">Premium Touch</h4>
                      <p className="text-gray-300 text-sm">Professional grooming with attention to detail</p>
                    </div>
                  </div>
                  <div className="flex items-start space-x-3">
                    <div className="w-6 h-6 bg-yellow-400 rounded-full flex items-center justify-center mt-1">
                      <span className="text-black text-sm font-bold">✓</span>
                    </div>
                    <div>
                      <h4 className="text-white font-semibold">Multiple Services</h4>
                      <p className="text-gray-300 text-sm">From cuts to treatments and nail services</p>
                    </div>
                  </div>
                  <div className="flex items-start space-x-3">
                    <div className="w-6 h-6 bg-yellow-400 rounded-full flex items-center justify-center mt-1">
                      <span className="text-black text-sm font-bold">✓</span>
                    </div>
                    <div>
                      <h4 className="text-white font-semibold">Training Available</h4>
                      <p className="text-gray-300 text-sm">Learn professional barbering skills</p>
                    </div>
                  </div>
                  <div className="flex items-start space-x-3">
                    <div className="w-6 h-6 bg-yellow-400 rounded-full flex items-center justify-center mt-1">
                      <span className="text-black text-sm font-bold">✓</span>
                    </div>
                    <div>
                      <h4 className="text-white font-semibold">Leisure Facilities</h4>
                      <p className="text-gray-300 text-sm">Enjoy snooker while you wait</p>
                    </div>
                  </div>
                </div>
              </div>
            </div>
          </div>
        )}
      </main>

      {/* Footer */}
      <footer className="bg-black/50 border-t border-yellow-400/20 mt-16">
        <div className="max-w-6xl mx-auto px-4 py-8 text-center">
          <div className="flex items-center justify-center space-x-3 mb-4">
            <div className="w-10 h-10 bg-gradient-to-r from-yellow-400 to-yellow-600 rounded-full flex items-center justify-center">
              <Scissors className="text-black" size={20} />
            </div>
            <div className="text-left">
              <h4 className="text-white font-bold">P-MONIZ BARBING SHOP</h4>
              <p className="text-yellow-400 text-sm">Barbing that Suites your Style</p>
            </div>
          </div>
          <p className="text-gray-400 text-sm">
            © 2024 P-Moniz Barbing Shop. Professional grooming services in Bayelsa State.
          </p>
        </div>
      </footer>
    </div>
  );
};

export default App;
