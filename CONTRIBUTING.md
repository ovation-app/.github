# Contributing to Ovation

Thank you for your interest in contributing to the Ovation project! This document provides guidelines and information for contributors across all Ovation repositories.

## 📋 Table of Contents

- [Code of Conduct](#code-of-conduct)
- [Getting Started](#getting-started)
- [Project Structure](#project-structure)
- [Contributing Guidelines](#contributing-guidelines)
- [Development Workflow](#development-workflow)
- [Coding Standards](#coding-standards)
- [Testing Guidelines](#testing-guidelines)
- [Documentation](#documentation)
- [Community](#community)

## 🤝 Code of Conduct

This project follows our [Code of Conduct](CODE_OF_CONDUCT.md). By participating, you are expected to uphold this code. Please report unacceptable behavior to [hello@ovation.network](mailto:hello@ovation.network).

## 🚀 Getting Started

### Prerequisites

Before contributing, ensure you have:

- **Git** - [Download here](https://git-scm.com/downloads)
- **Node.js 18+** (for frontend) - [Download here](https://nodejs.org/)
- **.NET 8.0 SDK** (for backend) - [Download here](https://dotnet.microsoft.com/download/dotnet/8.0)
- **MySQL 8.0+** (for backend) - [Download here](https://dev.mysql.com/downloads/mysql/)
- **Docker Desktop** (Optional) - [Download here](https://www.docker.com/products/docker-desktop/)

### Repository Structure

Ovation consists of two main repositories:

- **[ovation-mvp](https://github.com/ovation-app/ovation-mvp)** - Frontend React/Next.js application
- **[ovation-backend](https://github.com/ovation-app/ovation-backend)** - Backend ASP.NET Core API

### Development Setup

1. **Fork and Clone Repositories**
   ```bash
   # Fork both repositories on GitHub, then clone your forks
   git clone https://github.com/YOUR_USERNAME/ovation-mvp.git
   git clone https://github.com/YOUR_USERNAME/ovation-backend.git
   ```

2. **Set Up Frontend**
   ```bash
   cd ovation-mvp
   npm install
   npm run dev
   ```

3. **Set Up Backend**
   ```bash
   cd ovation-backend
   # Follow the detailed setup guide
   # See: https://github.com/ovation-app/ovation-backend/blob/main/Docs/INSTALLATION.md
   ```

## 📝 Contributing Guidelines

### Types of Contributions

We welcome various types of contributions:

#### 🐛 Bug Fixes
- Fix existing issues across frontend and backend
- Improve error handling and user experience
- Resolve performance issues
- Enhance security measures

#### ✨ New Features
- Add new blockchain integrations
- Implement additional social features
- Create new analytics and discovery tools
- Enhance the gamification system
- Add new UI/UX components

#### 📚 Documentation
- Improve API documentation
- Add code examples and tutorials
- Update setup guides
- Create video tutorials
- Enhance README files

#### 🧪 Testing
- Add unit and integration tests
- Improve test coverage
- Add end-to-end tests
- Performance and load testing
- Security testing

#### 🔧 Infrastructure
- Docker and deployment improvements
- CI/CD pipeline enhancements
- Monitoring and observability
- Security enhancements
- Performance optimizations

### Contribution Workflow

#### 1. Choose Your Focus
- **Frontend**: Work on React/Next.js components, UI/UX, user interactions
- **Backend**: Work on API endpoints, business logic, database operations
- **Full-stack**: Work on features that span both frontend and backend
- **Documentation**: Improve guides, tutorials, and API documentation

#### 2. Create a Branch
```bash
# For frontend changes
cd ovation-mvp
git checkout -b feature/your-feature-name

# For backend changes
cd ovation-backend
git checkout -b feature/your-feature-name
```

#### 3. Make Changes
- Follow the [coding standards](#coding-standards)
- Write tests for new functionality
- Update documentation as needed
- Ensure all tests pass

#### 4. Commit Changes
```bash
# Use conventional commit messages
git commit -m "feat: add new NFT search functionality

- Add SearchNftQueryHandler
- Implement pagination support
- Add comprehensive tests
- Update API documentation

Closes #123"
```

#### 5. Push and Create PR
```bash
git push origin feature/your-feature-name
# Create a Pull Request on GitHub
```

## 🔄 Development Workflow

### Frontend Development
- **Framework**: React 18 + Next.js 14
- **Language**: TypeScript
- **Styling**: Tailwind CSS + Radix UI
- **State Management**: React Query + Easy Peasy
- **Testing**: Jest + React Testing Library

### Backend Development
- **Framework**: ASP.NET Core 8.0
- **Architecture**: Clean Architecture + CQRS
- **Database**: MySQL + Entity Framework Core
- **Testing**: xUnit + NUnit
- **Documentation**: Swagger/OpenAPI

### Cross-Repository Changes
When working on features that span both repositories:

1. **Start with Backend**: Implement API endpoints first
2. **Update Frontend**: Consume new APIs
3. **Coordinate PRs**: Reference related PRs in descriptions
4. **Test Integration**: Ensure end-to-end functionality works

## 📏 Coding Standards

### General Principles
- **Clean Code**: Write readable, maintainable code
- **DRY Principle**: Don't Repeat Yourself
- **SOLID Principles**: Follow object-oriented design principles
- **Consistent Naming**: Use clear, descriptive names
- **Documentation**: Comment complex logic and public APIs

### Frontend Standards
```typescript
// Use TypeScript interfaces
interface UserProfile {
  id: string;
  username: string;
  displayName: string;
}

// Use functional components with hooks
const UserProfile: React.FC<UserProfileProps> = ({ user }) => {
  const [isLoading, setIsLoading] = useState(false);
  
  // Component logic here
  
  return (
    <div className="user-profile">
      {/* JSX here */}
    </div>
  );
};
```

### Backend Standards
```csharp
// Use async/await patterns
public async Task<ResponseData<User>> GetUserAsync(Guid userId)
{
    var user = await _userRepository.GetByIdAsync(userId);
    return ResponseData<User>.Success(user);
}

// Use dependency injection
public class UserController : BaseController
{
    private readonly IUserRepository _userRepository;
    
    public UserController(IServiceProvider service) : base(service) { }
}
```

## 🧪 Testing Guidelines

### Frontend Testing
```typescript
// Component testing
describe('UserProfile', () => {
  it('renders user information correctly', () => {
    const user = { id: '1', username: 'testuser' };
    render(<UserProfile user={user} />);
    expect(screen.getByText('testuser')).toBeInTheDocument();
  });
});

// API testing
describe('User API', () => {
  it('fetches user data successfully', async () => {
    const mockData = { id: '1', username: 'testuser' };
    mockApi.get('/api/user/1').mockResolvedValue(mockData);
    
    const result = await userApi.getUser('1');
    expect(result).toEqual(mockData);
  });
});
```

### Backend Testing
```csharp
[Test]
public async Task GetUser_WithValidId_ReturnsUser()
{
    // Arrange
    var userId = Guid.NewGuid();
    var expectedUser = new User { Id = userId, Username = "testuser" };
    _mockRepository.Setup(r => r.GetByIdAsync(userId))
                   .ReturnsAsync(expectedUser);

    // Act
    var result = await _handler.Handle(new GetUserQuery(userId), CancellationToken.None);

    // Assert
    Assert.That(result.Status, Is.True);
    Assert.That(result.Data.Username, Is.EqualTo("testuser"));
}
```

## 📚 Documentation

### Code Documentation
- **XML Comments**: Document all public APIs
- **README Updates**: Update relevant README files
- **API Documentation**: Keep Swagger documentation current
- **Architecture Docs**: Update ADRs when making architectural changes

### Documentation Types
- **Setup Guides**: Installation and configuration
- **API Documentation**: Endpoint descriptions and examples
- **Architecture Docs**: System design and patterns
- **Tutorials**: Step-by-step guides for common tasks
- **Troubleshooting**: Common issues and solutions

## 🏷️ Good First Issues

Looking for your first contribution? Check out these beginner-friendly areas:

### Frontend
- [ ] Improve component documentation
- [ ] Add loading states to components
- [ ] Enhance error handling in forms
- [ ] Add accessibility improvements
- [ ] Create reusable UI components

### Backend
- [ ] Add input validation to endpoints
- [ ] Improve error messages
- [ ] Add unit tests for existing features
- [ ] Enhance API documentation
- [ ] Add logging improvements

### Documentation
- [ ] Improve setup guides
- [ ] Add code examples
- [ ] Create video tutorials
- [ ] Update API documentation
- [ ] Add troubleshooting guides

## 🤝 Community

### Communication Channels
- **GitHub Issues**: Bug reports and feature requests
- **GitHub Discussions**: General discussions and questions
- **Discord**: Real-time community chat (http://discord.gg/E3gZdW727H)
- **Email**: [hello@ovation.network](mailto:hello@ovation.network)

### Getting Help
1. **Check Documentation**: Review existing documentation first
2. **Search Issues**: Look for similar issues or discussions
3. **Ask Questions**: Use GitHub Discussions for questions
4. **Join Community**: Participate in community discussions

### Recognition
Contributors are recognized in:
- **[CONTRIBUTORS.md](CONTRIBUTORS.md)**: List of all contributors
- **Release Notes**: Feature contributors mentioned
- **Community Hall of Fame**: Outstanding contributors

## 📋 Checklist for Contributors

### Before Contributing
- [ ] Read and understand the Code of Conduct
- [ ] Set up development environment
- [ ] Understand the project architecture
- [ ] Review existing issues and discussions
- [ ] Choose appropriate repository (frontend/backend)

### During Development
- [ ] Follow coding standards
- [ ] Write comprehensive tests
- [ ] Update documentation
- [ ] Consider performance implications
- [ ] Review security implications
- [ ] Test cross-repository integration (if applicable)

### Before Submitting
- [ ] Self-review your code
- [ ] Run all tests locally
- [ ] Update documentation
- [ ] Create descriptive PR
- [ ] Link related issues
- [ ] Ensure CI/CD passes

## 🎉 Thank You!

Thank you for contributing to Ovation! Your contributions help make this project better for everyone. We appreciate your time and effort in building the future of NFT social interaction.

---

**Questions?** Feel free to reach out via [GitHub Discussions](https://github.com/ovation-app/ovation-backend/discussions) or [email](mailto:hello@ovation.network).
