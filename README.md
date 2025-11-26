import React, { useState, useEffect } from 'react';
import { Menu, X, TrendingUp, Users, BarChart3, DollarSign, Bell, Settings, LogOut, Send, ChevronRight, Star, Play } from 'lucide-react';
import { LineChart, Line, BarChart, Bar, XAxis, YAxis, CartesianGrid, Tooltip, ResponsiveContainer, PieChart, Pie, Cell } from 'recharts';

export default function BusinessWebsite() {
  const [currentPage, setCurrentPage] = useState('home');
  const [sidebarOpen, setSidebarOpen] = useState(true);
  const [activeTab, setActiveTab] = useState('dashboard');
  const [realtimeData, setRealtimeData] = useState([]);
  const [stats, setStats] = useState({ revenue: 0, users: 0, growth: 0 });
  const [messages, setMessages] = useState([
    { id: 1, user: 'Sarah Chen', message: 'Project update ready', time: '2:30 PM' },
    { id: 2, user: 'Mike Johnson', message: 'Meeting scheduled for 4 PM', time: '1:15 PM' }
  ]);
  const [newMessage, setNewMessage] = useState('');
  const [scrollY, setScrollY] = useState(0);

  useEffect(() => {
    const handleScroll = () => setScrollY(window.scrollY);
    window.addEventListener('scroll', handleScroll);
    return () => window.removeEventListener('scroll', handleScroll);
  }, []);

  useEffect(() => {
    if (currentPage === 'dashboard') {
      const interval = setInterval(() => {
        setRealtimeData(prev => {
          const newData = [...prev, {
            time: new Date().toLocaleTimeString(),
            revenue: Math.floor(Math.random() * 5000) + 2000,
            conversions: Math.floor(Math.random() * 150) + 50
          }];
          return newData.slice(-10);
        });

        setStats(prev => ({
          revenue: prev.revenue + Math.floor(Math.random() * 500),
          users: prev.users + Math.floor(Math.random() * 5),
          growth: (Math.random() * 8 + 2).toFixed(1)
        }));
      }, 2000);

      return () => clearInterval(interval);
    }
  }, [currentPage]);

  const handleSendMessage = () => {
    if (newMessage.trim()) {
      setMessages(prev => [...prev, {
        id: prev.length + 1,
        user: 'You',
        message: newMessage,
        time: new Date().toLocaleTimeString([], { hour: '2-digit', minute: '2-digit' })
      }]);
      setNewMessage('');
    }
  };

  const chartData = [
    { name: 'Mon', value: 4000 },
    { name: 'Tue', value: 3000 },
    { name: 'Wed', value: 2000 },
    { name: 'Thu', value: 2780 },
    { name: 'Fri', value: 1890 },
    { name: 'Sat', value: 2390 },
    { name: 'Sun', value: 3490 }
  ];

  const pieData = [
    { name: 'Product A', value: 40 },
    { name: 'Product B', value: 30 },
    { name: 'Product C', value: 20 },
    { name: 'Product D', value: 10 }
  ];

  const COLORS = ['#3b82f6', '#10b981', '#f59e0b', '#ef4444'];

  const features = [
    { icon: '📊', title: 'Real-time Analytics', desc: 'Monitor your business metrics live' },
    { icon: '👥', title: 'User Management', desc: 'Track and manage your customer base' },
    { icon: '💰', title: 'Revenue Tracking', desc: 'Detailed financial insights and reports' },
    { icon: '🚀', title: 'Performance', desc: 'Lightning-fast dashboard performance' }
  ];

  const testimonials = [
    { name: 'John Doe', role: 'CEO', company: 'Tech Corp', text: 'Amazing platform! Increased our productivity by 40%' },
    { name: 'Jane Smith', role: 'Manager', company: 'Business Inc', text: 'Best investment we made this year' },
    { name: 'Mike Wilson', role: 'Director', company: 'Growth Co', text: 'Excellent support and features' }
  ];

  const pricingPlans = [
    { name: 'Starter', price: '$29', features: ['5 Users', 'Basic Analytics', 'Email Support', '5GB Storage'] },
    { name: 'Professional', price: '$79', features: ['25 Users', 'Advanced Analytics', 'Priority Support', '100GB Storage'], popular: true },
    { name: 'Enterprise', price: '$199', features: ['Unlimited Users', 'Custom Analytics', '24/7 Support', 'Unlimited Storage'] }
  ];

  if (currentPage === 'home') {
    return (
      <div className="bg-gray-900 text-white overflow-hidden">
        {/* Navbar */}
        <nav className={`fixed w-full z-50 transition-all duration-300 ${scrollY > 50 ? 'bg-gray-900 shadow-lg' : 'bg-transparent'}`}>
          <div className="max-w-7xl mx-auto px-6 py-4 flex justify-between items-center">
            <div className="text-2xl font-bold bg-gradient-to-r from-blue-400 to-purple-500 bg-clip-text text-transparent">
              BizHub
            </div>
            <div className="hidden md:flex space-x-8">
              <button onClick={() => setCurrentPage('home')} className="hover:text-blue-400 transition">Home</button>
              <button className="hover:text-blue-400 transition">Features</button>
              <button className="hover:text-blue-400 transition">Pricing</button>
              <button className="hover:text-blue-400 transition">Contact</button>
            </div>
            <button onClick={() => setCurrentPage('dashboard')} className="bg-blue-600 hover:bg-blue-700 px-6 py-2 rounded-lg transition">
              Dashboard
            </button>
          </div>
        </nav>

        {/* Hero Section */}
        <section className="min-h-screen flex items-center justify-center px-6 relative overflow-hidden pt-20">
          <div className="absolute inset-0 bg-gradient-to-b from-blue-900/20 to-transparent"></div>
          <div className="max-w-4xl mx-auto text-center relative z-10">
            <div className="mb-6 inline-block">
              <span className="px-4 py-2 bg-blue-900/50 border border-blue-700 rounded-full text-sm">✨ Welcome to BizHub</span>
            </div>
            <h1 className="text-6xl md:text-7xl font-bold mb-6 leading-tight">
              Business Intelligence <span className="bg-gradient-to-r from-blue-400 to-purple-500 bg-clip-text text-transparent">Simplified</span>
            </h1>
            <p className="text-xl text-gray-300 mb-8 max-w-2xl mx-auto">
              Manage your business with powerful real-time analytics, beautiful dashboards, and actionable insights. All in one platform.
            </p>
            <div className="flex gap-4 justify-center flex-wrap">
              <button onClick={() => setCurrentPage('dashboard')} className="bg-blue-600 hover:bg-blue-700 px-8 py-4 rounded-lg text-lg font-semibold transition transform hover:scale-105">
                Get Started Free
              </button>
              <button className="border border-blue-500 hover:bg-blue-900/20 px-8 py-4 rounded-lg text-lg font-semibold transition flex items-center gap-2">
                <Play size={20} /> Watch Demo
              </button>
            </div>
          </div>

          {/* Floating Cards */}
          <div className="absolute top-32 right-10 w-64 h-48 bg-gradient-to-br from-purple-600/20 to-blue-600/20 rounded-2xl border border-purple-500/30 backdrop-blur p-6 hidden lg:block">
            <div className="text-sm text-gray-300">Real-time Revenue</div>
            <div className="text-3xl font-bold mt-2">${(50000 + stats.revenue).toLocaleString()}</div>
            <div className="text-green-400 text-sm mt-2">↑ {stats.growth}% this month</div>
          </div>

          <div className="absolute bottom-32 left-10 w-64 h-48 bg-gradient-to-br from-blue-600/20 to-green-600/20 rounded-2xl border border-green-500/30 backdrop-blur p-6 hidden lg:block">
            <div className="text-sm text-gray-300">Active Users</div>
            <div className="text-3xl font-bold mt-2">{(5000 + stats.users).toLocaleString()}</div>
            <div className="text-green-400 text-sm mt-2">Growing daily</div>
          </div>
        </section>

        {/* Features Section */}
        <section className="py-20 px-6">
          <div className="max-w-6xl mx-auto">
            <h2 className="text-4xl font-bold text-center mb-16">Powerful Features</h2>
            <div className="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-4 gap-8">
              {features.map((feature, i) => (
                <div key={i} className="bg-gray-800 border border-gray-700 rounded-xl p-8 hover:border-blue-500 transition group">
                  <div className="text-4xl mb-4">{feature.icon}</div>
                  <h3 className="text-xl font-semibold mb-2">{feature.title}</h3>
                  <p className="text-gray-400">{feature.desc}</p>
                  <div className="mt-4 flex items-center text-blue-400 opacity-0 group-hover:opacity-100 transition">
                    Learn more <ChevronRight size={16} className="ml-2" />
                  </div>
                </div>
              ))}
            </div>
          </div>
        </section>

        {/* Testimonials Section */}
        <section className="py-20 px-6 bg-gray-800/50">
          <div className="max-w-6xl mx-auto">
            <h2 className="text-4xl font-bold text-center mb-16">What Our Users Say</h2>
            <div className="grid grid-cols-1 md:grid-cols-3 gap-8">
              {testimonials.map((testimonial, i) => (
                <div key={i} className="bg-gray-800 rounded-xl p-8 border border-gray-700">
                  <div className="flex gap-1 mb-4">
                    {[...Array(5)].map((_, j) => <Star key={j} size={16} className="fill-yellow-400 text-yellow-400" />)}
                  </div>
                  <p className="text-gray-300 mb-6">"{testimonial.text}"</p>
                  <div>
                    <p className="font-semibold">{testimonial.name}</p>
                    <p className="text-sm text-gray-400">{testimonial.role} at {testimonial.company}</p>
                  </div>
                </div>
              ))}
            </div>
          </div>
        </section>

        {/* Pricing Section */}
        <section className="py-20 px-6">
          <div className="max-w-6xl mx-auto">
            <h2 className="text-4xl font-bold text-center mb-16">Simple, Transparent Pricing</h2>
            <div className="grid grid-cols-1 md:grid-cols-3 gap-8">
              {pricingPlans.map((plan, i) => (
                <div key={i} className={`rounded-xl p-8 border transition transform hover:scale-105 ${
                  plan.popular 
                    ? 'bg-gradient-to-br from-blue-600 to-purple-600 border-blue-400 relative' 
                    : 'bg-gray-800 border-gray-700'
                }`}>
                  {plan.popular && <div className="absolute top-0 left-1/2 transform -translate-x-1/2 -translate-y-1/2 bg-yellow-400 text-black px-4 py-1 rounded-full text-sm font-semibold">Most Popular</div>}
                  <h3 className="text-2xl font-bold mb-2">{plan.name}</h3>
                  <div className="text-4xl font-bold mb-6">{plan.price}<span className="text-lg text-gray-300">/mo</span></div>
                  <ul className="space-y-4 mb-8">
                    {plan.features.map((feature, j) => (
                      <li key={j} className="flex items-center gap-2">
                        <ChevronRight size={16} className="text-green-400" /> {feature}
                      </li>
                    ))}
                  </ul>
                  <button className={`w-full py-3 rounded-lg font-semibold transition ${
                    plan.popular ? 'bg-white text-blue-600 hover:bg-gray-200' : 'bg-blue-600 hover:bg-blue-700'
                  }`}>
                    Get Started
                  </button>
                </div>
              ))}
            </div>
          </div>
        </section>

        {/* CTA Section */}
        <section className="py-20 px-6 bg-gradient-to-r from-blue-600 to-purple-600">
          <div className="max-w-4xl mx-auto text-center">
            <h2 className="text-4xl font-bold mb-6">Ready to Transform Your Business?</h2>
            <p className="text-lg text-blue-100 mb-8">Join thousands of companies using BizHub to make smarter decisions.</p>
            <button onClick={() => setCurrentPage('dashboard')} className="bg-white text-blue-600 hover:bg-gray-100 px-8 py-4 rounded-lg text-lg font-semibold transition transform hover:scale-105">
              Start Your Free Trial Today
            </button>
          </div>
        </section>

        {/* Footer */}
        <footer className="bg-gray-800 border-t border-gray-700 px-6 py-12">
          <div className="max-w-6xl mx-auto grid grid-cols-1 md:grid-cols-4 gap-8 mb-8">
            <div>
              <h4 className="font-bold mb-4">BizHub</h4>
              <p className="text-gray-400">Making business intelligence accessible to everyone.</p>
            </div>
            <div>
              <h4 className="font-bold mb-4">Product</h4>
              <ul className="space-y-2 text-gray-400 text-sm">
                <li className="hover:text-white cursor-pointer">Features</li>
                <li className="hover:text-white cursor-pointer">Pricing</li>
                <li className="hover:text-white cursor-pointer">Security</li>
              </ul>
            </div>
            <div>
              <h4 className="font-bold mb-4">Company</h4>
              <ul className="space-y-2 text-gray-400 text-sm">
                <li className="hover:text-white cursor-pointer">About</li>
                <li className="hover:text-white cursor-pointer">Blog</li>
                <li className="hover:text-white cursor-pointer">Careers</li>
              </ul>
            </div>
            <div>
              <h4 className="font-bold mb-4">Legal</h4>
              <ul className="space-y-2 text-gray-400 text-sm">
                <li className="hover:text-white cursor-pointer">Privacy</li>
                <li className="hover:text-white cursor-pointer">Terms</li>
                <li className="hover:text-white cursor-pointer">Contact</li>
              </ul>
            </div>
          </div>
          <div className="border-t border-gray-700 pt-8 text-center text-gray-400">
            <p>&copy; 2024 BizHub. All rights reserved.</p>
          </div>
        </footer>
      </div>
    );
  }

  // Dashboard View
  return (
    <div className="flex h-screen bg-gray-900 text-white">
      {/* Sidebar */}
      <div className={`${sidebarOpen ? 'w-64' : 'w-20'} bg-gray-800 transition-all duration-300 border-r border-gray-700`}>
        <div className="p-4 flex items-center justify-between">
          {sidebarOpen && <h1 className="text-xl font-bold">BizHub</h1>}
          <button onClick={() => setSidebarOpen(!sidebarOpen)} className="hover:bg-gray-700 p-2 rounded">
            {sidebarOpen ? <X size={20} /> : <Menu size={20} />}
          </button>
        </div>
        
        <nav className="mt-8 space-y-4">
          {[
            { id: 'dashboard', icon: BarChart3, label: 'Dashboard' },
            { id: 'analytics', icon: TrendingUp, label: 'Analytics' },
            { id: 'users', icon: Users, label: 'Users' },
            { id: 'revenue', icon: DollarSign, label: 'Revenue' }
          ].map(item => (
            <button
              key={item.id}
              onClick={() => setActiveTab(item.id)}
              className={`w-full flex items-center space-x-3 px-4 py-3 transition ${
                activeTab === item.id ? 'bg-blue-600' : 'hover:bg-gray-700'
              }`}
            >
              <item.icon size={20} />
              {sidebarOpen && <span>{item.label}</span>}
            </button>
          ))}
        </nav>
      </div>

      {/* Main Content */}
      <div className="flex-1 flex flex-col overflow-hidden">
        {/* Top Nav */}
        <div className="bg-gray-800 border-b border-gray-700 px-8 py-4 flex justify-between items-center">
          <h2 className="text-2xl font-bold capitalize">{activeTab}</h2>
          <div className="flex items-center space-x-4">
            <button className="hover:bg-gray-700 p-2 rounded transition">
              <Bell size={20} />
            </button>
            <button className="hover:bg-gray-700 p-2 rounded transition">
              <Settings size={20} />
            </button>
            <button onClick={() => setCurrentPage('home')} className="hover:bg-gray-700 p-2 rounded transition">
              <LogOut size={20} />
            </button>
          </div>
        </div>

        {/* Content Area */}
        <div className="flex-1 overflow-auto p-8">
          {activeTab === 'dashboard' && (
            <div className="space-y-6">
              <div className="grid grid-cols-1 md:grid-cols-3 gap-6">
                <div className="bg-gradient-to-br from-blue-600 to-blue-800 p-6 rounded-lg">
                  <div className="flex justify-between items-start">
                    <div>
                      <p className="text-gray-200 text-sm">Revenue</p>
                      <p className="text-3xl font-bold">${stats.revenue.toLocaleString()}</p>
                    </div>
                    <DollarSign size={32} className="opacity-50" />
                  </div>
                  <p className="text-green-300 text-sm mt-4">↑ {stats.growth}% from last month</p>
                </div>

                <div className="bg-gradient-to-br from-green-600 to-green-800 p-6 rounded-lg">
                  <div className="flex justify-between items-start">
                    <div>
                      <p className="text-gray-200 text-sm">Active Users</p>
                      <p className="text-3xl font-bold">{(5000 + stats.users).toLocaleString()}</p>
                    </div>
                    <Users size={32} className="opacity-50" />
                  </div>
                  <p className="text-green-300 text-sm mt-4">↑ {stats.users} new today</p>
                </div>

                <div className="bg-gradient-to-br from-purple-600 to-purple-800 p-6 rounded-lg">
                  <div className="flex justify-between items-start">
                    <div>
                      <p className="text-gray-200 text-sm">Conversion Rate</p>
                      <p className="text-3xl font-bold">{stats.growth}%</p>
                    </div>
                    <TrendingUp size={32} className="opacity-50" />
                  </div>
                  <p className="text-green-300 text-sm mt-4">↑ Trending up</p>
                </div>
              </div>

              <div className="grid grid-cols-1 lg:grid-cols-2 gap-6">
                <div className="bg-gray-800 p-6 rounded-lg border border-gray-700">
                  <h3 className="text-lg font-semibold mb-4">Real-time Activity</h3>
                  <ResponsiveContainer width="100%" height={250}>
                    <LineChart data={realtimeData}>
                      <CartesianGrid strokeDasharray="3 3" stroke="#444" />
                      <XAxis dataKey="time" stroke="#999" />
                      <YAxis stroke="#999" />
                      <Tooltip contentStyle={{ backgroundColor: '#1f2937', border: 'none' }} />
                      <Line type="monotone" dataKey="revenue" stroke="#3b82f6" strokeWidth={2} />
                    </LineChart>
                  </ResponsiveContainer>
                </div>

                <div className="bg-gray-800 p-6 rounded-lg border border-gray-700">
                  <h3 className="text-lg font-semibold mb-4">Weekly Performance</h3>
                  <ResponsiveContainer width="100%" height={250}>
                    <BarChart data={chartData}>
                      <CartesianGrid strokeDasharray="3 3" stroke="#444" />
                      <XAxis dataKey="name" stroke="#999" />
                      <YAxis stroke="#999" />
                      <Tooltip contentStyle={{ backgroundColor: '#1f2937', border: 'none' }} />
                      <Bar dataKey="value" fill="#10b981" />
                    </BarChart>
                  </ResponsiveContainer>
                </div>
              </div>

              <div className="grid grid-cols-1 lg:grid-cols-2 gap-6">
                <div className="bg-gray-800 p-6 rounded-lg border border-gray-700">
                  <h3 className="text-lg font-semibold mb-4">Product Distribution</h3>
                  <ResponsiveContainer width="100%" height={250}>
                    <PieChart>
                      <Pie data={pieData} cx="50%" cy="50%" labelLine={false} label outerRadius={80} fill="#8884d8" dataKey="value">
                        {pieData.map((entry, index) => (
                          <Cell key={`cell-${index}`} fill={COLORS[index % COLORS.length]} />
                        ))}
                      </Pie>
                      <Tooltip />
                    </PieChart>
                  </ResponsiveContainer>
                </div>

                <div className="bg-gray-800 p-6 rounded-lg border border-gray-700 flex flex-col">
                  <h3 className="text-lg font-semibold mb-4">Messages</h3>
                  <div className="flex-1 overflow-y-auto space-y-3 mb-4">
                    {messages.map(msg => (
                      <div key={msg.id} className="bg-gray-700 p-3 rounded text-sm">
                        <p className="font-semibold text-blue-400">{msg.user}</p>
                        <p className="text-gray-300">{msg.message}</p>
                        <p className="text-gray-500 text-xs mt-1">{msg.time}</p>
                      </div>
                    ))}
                  </div>
                  <div className="flex gap-2">
                    <input
                      type="text"
                      value={newMessage}
                      onChange={(e) => setNewMessage(e.target.value)}
                      onKeyPress={(e) => e.key === 'Enter' && handleSendMessage()}
                      placeholder="Type message..."
                      className="flex-1 bg-gray-700 rounded px-3 py-2 text-sm focus:outline-none focus:ring-2 focus:ring-blue-500"
                    />
                    <button onClick={handleSendMessage} className="bg-blue-600 hover:bg-blue-700 p-2 rounded transition">
                      <Send size={18} />
                    </button>
                  </div>
                </div>
              </div>
            </div>
          )}

          {activeTab === 'analytics' && (
            <div className="bg-gray-800 p-6 rounded-lg border border-gray-700">
              <h3 className="text-2xl font-semibold mb-6">Analytics Overview</h3>
              <ResponsiveContainer width="100%" height={400}>
                <BarChart data={chartData}>
                  <CartesianGrid strokeDasharray="3 3" stroke="#444" />
                  <XAxis dataKey="name" stroke="#999" />
                  <YAxis stroke="#999" />
                  <Tooltip contentStyle={{ backgroundColor: '#1f2937', border: 'none' }} />
                  <Bar dataKey="value" fill="#3b82f6" radius={[8, 8, 0, 0]} />
                </BarChart>
              </ResponsiveContainer>
            </div>
          )}

          {activeTab === 'users' && (
            <div className="grid grid-cols-1 md:grid-cols-2 gap-6">
              {[...Array(4)].map((_, i) => (
                <div key={i} className="bg-gray-800 p-6 rounded-lg border border-gray-700">
                  <div className="flex items-center space-x-4">
                    <div className="w-12 h-12 bg-gradient-to-br from-blue-500 to-purple-500 rounded-full"></div>
                    <div className="flex-1">
                      <p className="font-semibold">User {i + 1}</p>
                      <p className="text-gray-400 text-sm">user{i + 1}@email.com</p>
                    </div>
                    <span className="px-3 py-1 bg-green-900 text-green-300 rounded text-sm">Active</span>
                  </div>
                </div>
              ))}
            </div>
          )}

          {activeTab === 'revenue' && (
            <div className="space-y-6">
              <div className="grid grid-cols-1 md:grid-cols-2 gap-6">
                <div className="bg-gray-800 p-6 rounded-lg border border-gray-700">
                  <h3 className="text-lg font-semibold mb-4">Revenue Trend</h3>
                  <ResponsiveContainer width="100%" height={300}>
                    <LineChart data={chartData}>
                      <CartesianGrid strokeDasharray="3 3" stroke="#444" />
                      <XAxis dataKey="name" stroke="#999" />
                      <YAxis stroke="#999" />
                      <Tooltip contentStyle={{ backgroundColor: '#1f2937', border: 'none' }} />
                      <Line type="monotone" dataKey="value" stroke="#f59e0b" strokeWidth={2} />
                    </LineChart>
                  </ResponsiveContainer>
                </div>

                <div className="bg-gray-800 p-6 rounded-lg border border-gray-700">
                  <h3 className="text-lg font-semibold mb-4">Revenue by Source</h3>
                  <ResponsiveContainer width="100%" height={300}>
                    <PieChart>
                      <Pie data={pieData} cx="50%" cy="50%" outerRadius={80} fill="#8884d8" dataKey="value">
                        {pieData.map((entry, index) => (
                          <Cell key={`cell-${index}`} fill={COLORS[index % COLORS.length]} />
                        ))}
                      </Pie>
                      <Tooltip />
                    </PieChart>
                  </ResponsiveContainer>
                </div>
              </div>
            </div>
          )}
        </div>
      </div>
    </div>
  );
}
